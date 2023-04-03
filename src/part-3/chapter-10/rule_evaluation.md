## **Rule Evaluation**

Borgmon is really just a programmable calculator, with some syntactic sugar that enables it to generate alerts. The data collection and storage components already described are just necessary evils to make that programmable calculator ultimately fit for purpose here as a monitoring system. :)

> Centralizing the rule evaluation in a monitoring system, rather than delegating it to forked subprocesses, means that computations can run in parallel against many similar targets. This practice keeps the configuration relatively small in size (for example, by removing duplication of code) yet more powerful through its expressiveness.

The Borgmon program code, also known as Borgmon rules, consists of simple algebraic expressions that compute time-series from other time-series. These rules can be quite powerful because they can query the history of a single time-series (i.e., the time axis), query different subsets of labels from many time-series at once (i.e., the space axis), and apply many mathematical operations.

Rules run in a parallel threadpool where possible, but are dependent on ordering when using previously defined rules as input. The size of the vectors returned by their query expressions also determines the overall runtime of a rule. Thus, it is typically the case that one can add CPU resources to a Borgmon task in response to it running slow. To assist more detailed analysis, internal metrics on the runtime of rules are exported for performance debugging and for monitoring the monitoring.

Aggregation is the cornerstone of rule evaluation in a distributed environment. Aggregation entails taking the sum of a set of time-series from the tasks in a job in order to treat the job as a whole. From those sums, overall rates can be computed. For example, the total queries-per-second rate of a job in a datacenter is the sum of all the rates of change11 of all the query counters.

> A counter is any nonmonotonically decreasing variable—which is to say, counters only increase in value. Gauges, on the other hand, may take any value they like. Counters measure increasing values, such as the total number of kilometers driven, while gauges show current state, such as the amount of fuel remaining or current speed. When collecting Borgmon-style data, it’s better to use counters, because they don’t lose meaning when events occur between sampling intervals. Should any activity or changes occur between sampling intervals, a gauge collection is likely to miss that activity.

For an example web server, we might want to alert when our web server cluster starts to serve more errors as a percent of requests than we think is normal—or more technically, when the sum of the rates of non-HTTP-200 return codes on all tasks in the cluster, divided by the sum of the rates of requests to all tasks in that cluster, is greater than some value.

This is accomplished by:

1. Aggregating the rates of response codes across all tasks, outputting a vector of rates at that point in time, one for each code.
2. Computing the total error rate as the sum of that vector, outputting a single value for the cluster at that point in time. This total error rate excludes the 200 code from the sum, because it is not an error.
3. Computing the cluster-wide ratio of errors to requests, dividing the total error rate by the rate of requests that arrived, and again outputting a single value for the cluster at that point in time.

Each of these outputs at a point in time gets appended to its named variable expression, which creates the new time-series. As a result, we will be able to inspect the history of error rates and error ratios some other time.

The rate of requests rules would be written in Borgmon’s rule language as the following:

```bash
    rules <<<
      # Compute the rate of requests for each task from the count of requests
      {var=task:http_requests:rate10m,job=webserver} =
        rate({var=http_requests,job=webserver}[10m]);
      # Sum the rates to get the aggregate rate of queries for the cluster;
      # ‘without instance’ instructs Borgmon to remove the instance label
      # from the right hand side.
      {var=dc:http_requests:rate10m,job=webserver} =
        sum without instance({var=task:http_requests:rate10m,job=webserver})
    >>>
```

The rate() function takes the enclosed expression and returns the total delta divided by the total time between the earliest and latest values.

With the example time-series data from the query before, the results for the task:http_requests:rate10m rule would look like:

`{var=task:http_requests:rate10m,job=webserver,instance=host0:80, ...} 1`

`{var=task:http_requests:rate10m,job=webserver,instance=host2:80, ...} 0.9`

`{var=task:http_requests:rate10m,job=webserver,instance=host3:80, ...} 1.1`

`{var=task:http_requests:rate10m,job=webserver,instance=host4:80, ...} 0`

`{var=task:http_requests:rate10m,job=webserver,instance=host5:80, ...} 1`

and the results for the `dc:http_requests:rate10m` rule would be:

`{var=dc:http_requests:rate10m,job=webserver,service=web,zone=us-west} 4`

because the second rule uses the first one as input.

> The instance label is missing in the output now, discarded by the aggregation rule. If it had remained in the rule, then Borgmon would not have been able to sum the five rows together.

In these examples, we use a time window because we’re dealing with discrete points in the time-series, as opposed to continuous functions. Doing so makes the rate calculation easier than performing calculus, but means that to compute a rate, we need to select a sufficient number of data points. We also have to deal with the possibility that some recent collections have failed. Recall that the historical variable expression notation uses the range [10m] to avoid missing data points caused by collection errors.

The example also uses a Google convention that helps readability. Each computed variable name contains a colon-separated triplet indicating the aggregation level, the variable name, and the operation that created that name. In this example, the lefthand variables are "task HTTP requests 10-minute rate" and "datacenter HTTP requests 10-minute rate."

Now that we know how to create a rate of queries, we can build on that to also compute a rate of errors, and then we can calculate the ratio of responses to requests to understand how much useful work the service is doing. We can compare the ratio rate of errors to our service level objective (see Chapter 4) and alert if this objective is missed or in danger of being missed:

```perl
    rules <<<
       # Compute a rate pertask and per ‘code’ label
       {var=task:http_responses:rate10m,job=webserver} =
         rate by code({var=http_responses,job=webserver}[10m]);
       # Compute a cluster level response rate per ‘code’ label
       {var=dc:http_responses:rate10m,job=webserver} =
         sum without instance({var=task:http_responses:rate10m,job=webserver});
       # Compute a new cluster level rate summing all non 200 codes
       {var=dc:http_errors:rate10m,job=webserver} = sum without code(
         {var=dc:http_responses:rate10m,jobwebserver,code=!/200/};
       # Compute the ratio of the rate of errors to the rate of requests
       {var=dc:http_errors:ratio_rate10m,job=webserver} =
         {var=dc:http_errors:rate10m,job=webserver}
           /
         {var=dc:http_requests:rate10m,job=webserver};
     >>>
```

Again, this calculation demonstrates the convention of suffixing the new time-series variable name with the operation that created it. This result is read as "datacenter HTTP errors 10 minute ratio of rates."

The output of these rules might look like:

```perl
{var=task:http_responses:rate10m,job=webserver}
    {var=task:http_responses:rate10m,job=webserver,code=200,instance=host0:80, ...} 1
    {var=task:http_responses:rate10m,job=webserver,code=500,instance=host0:80, ...} 0
    {var=task:http_responses:rate10m,job=webserver,code=200,instance=host1:80, ...} 0.5
    {var=task:http_responses:rate10m,job=webserver,code=500,instance=host1:80, ...} 0.4
    {var=task:http_responses:rate10m,job=webserver,code=200,instance=host2:80, ...} 1
    {var=task:http_responses:rate10m,job=webserver,code=500,instance=host2:80, ...} 0.1
    {var=task:http_responses:rate10m,job=webserver,code=200,instance=host3:80, ...} 0
    {var=task:http_responses:rate10m,job=webserver,code=500,instance=host3:80, ...} 0
    {var=task:http_responses:rate10m,job=webserver,code=200,instance=host4:80, ...} 0.9
    {var=task:http_responses:rate10m,job=webserver,code=500,instance=host4:80, ...} 0.1
{var=dc:http_responses:rate10m,job=webserver}
    {var=dc:http_responses:rate10m,job=webserver,code=200, ...} 3.4
    {var=dc:http_responses:rate10m,job=webserver,code=500, ...} 0.6
{var=dc:http_responses:rate10m,jobwebserver,code=!/200/}
    {var=dc:http_responses:rate10m,job=webserver,code=500, ...} 0.6
{var=dc:http_errors:rate10m,job=webserver}
    {var=dc:http_errors:rate10m,job=webserver, ...} 0.6
{var=dc:http_errors:ratio_rate10m,job=webserver}
    {var=dc:http_errors:ratio_rate10m,job=webserver} 0.15
```

> The preceding output shows the intermediate query in the `dc:http_errors:rate10m` rule that filters the non-200 error codes. Though the value of the expressions are the same, observe that the code label is retained in one but removed from the other.

As mentioned previously, Borgmon rules create new time-series, so the results of the computations are kept in the time-series arena and can be inspected just as the source time-series are. The ability to do so allows for ad hoc querying, evaluation, and exploration as tables or charts. This is a useful feature for debugging while on-call, and if these ad hoc queries prove useful, they can be made permanent visualizations on a service console.
