## **Alerting**

When an alerting rule is evaluated by a Borgmon, the result is either true, in which case the alert is triggered, or false. Experience shows that alerts can “flap” (toggle their state quickly); therefore, the rules allow a minimum duration for which the alerting rule must be true before the alert is sent. Typically, this duration is set to at least two rule evaluation cycles to ensure no missed collections cause a false alert.

The following example creates an alert when the error ratio over 10 minutes exceeds 1% and the total number of errors exceeds 1:

```perl
rules <<<
      {var=dc:http_errors:ratio_rate10m,job=webserver} > 0.01
        and by job, error
      {var=dc:http_errors:rate10m,job=webserver} > 1
        for 2m
        => ErrorRatioTooHigh
          details "webserver error ratio at [[trigger_value]]"
          labels {severity=page};
    >>>
```

Our example holds the ratio rate at 0.15, which is well over the threshold of 0.01 in the alerting rule. However, the number of errors is not greater than 1 at this moment, so the alert won’t be active. Once the number of errors exceeds 1, the alert will go pending for two minutes to ensure it isn’t a transient state, and only then will it fire.

The alert rule contains a small template for filling out a message containing contex‐ tual information: which job the alert is for, the name of the alert, the numerical value of the triggering rule, and so on. The contextual information is filled out by Borgmon when the alert fires and is sent in the Alert RPC.

Borgmon is connected to a centrally run service, known as the Alertmanager, which receives Alert RPCs when the rule first triggers, and then again when the alert is con‐ sidered to be “firing.” The Alertmanager is responsible for routing the alert notifica‐ tion to the correct destination. Alertmanager can be configured to do the following:

* Inhibit certain alerts when others are active
* Deduplicate alerts from multiple Borgmon that have the same labelsets
* Fan-in or fan-out alerts based on their labelsets when multiple alerts with similar labelsets fire

As described in Chapter 6, teams send their page-worthy alerts to their on-call rota‐ tion and their important but subcritical alerts to their ticket queues. All other alerts should be retained as informational data for status dashboards.

A more comprehensive guide to alert design can be found in Chapter 4.
