---
title: "Viewing function monitoring charts in {{ sf-full-name }}"
description: "You can view a monitoring chart in {{ sf-full-name }} using the management console. To do this, select {{ sf-name }} and click the function to view monitoring charts for."
---

# Viewing function monitoring charts

 You can monitor functions at runtime using the monitoring tools in your management console. These tools display diagnostic information in the form of charts. Metric values are collected and charts are displayed by [{{ monitoring-name }}](../../../monitoring/). 

The chart update period is 15 seconds.

## Viewing monitoring charts {#charts}

{% list tabs %}

- Management console

   1. In the [management console]({{ link-console-main }}), select the folder containing your function.

   1. Select **{{ ui-key.yacloud.iam.folder.dashboard.label_serverless-functions }}**.

   1. Select a function to view its monitoring charts.

   1. Go to the **{{ ui-key.yacloud.serverless-functions.item.switch_monitoring }}** tab.

   1. The following charts will open on the page:

      * **Requests**: Number of function calls.
      * **Request latency**: Average time it takes a trigger to process a request.
      * **Errors**: The number of runtime errors a function generated.

   You can select the time period to display information for: hour, day, week, month, or a custom interval.

{% endlist %}

## Custom {#metrics} metrics

 To get started with [metrics](../../../monitoring/concepts/data-model.md#metric), [dashboards](../../../monitoring/concepts/visualization/dashboard.md), and [alerts](../../../monitoring/concepts/alerting.md#alert) in {{ monitoring-name }}, in the upper-right corner, click **{{ ui-key.yacloud.monitoring.button_open-in-monitoring }}**. 

| Metric name | Units | Explanations |
|----|----|----|
| `serverless.functions.inflight` | Invocations | Number of concurrent function invocations. |
| `serverless.functions.started_per_second` | Calls per second | Function call frequency. |
| `serverless.functions.finished_per_second` | Calls per second | Frequency of completing function invocation processing. |
| `serverless.functions.errors_per_second` | Errors per second | Error frequency when processing function invocations. |
| `serverless.functions.initializations_per_second` | Initializations per second | Frequency of new function instance initialization. |
| `serverless.functions.execution_time_milliseconds` | Calls per second | Function invocation frequency distribution histogram by request processing time in milliseconds. Request processing time intervals are shown in the `bin` label. |
| `serverless.functions.used_memory_bytes` | Calls per second | Function invocation frequency distribution histogram by memory used in bytes. Intervals of the RAM used by the request are shown in the `bin` label. |

### Custom metrics labels {#labels}

| Label name | Possible values | Explanations |
|----|----|----|
| `function` | Function name | The label contains the name of the function that the metric values refer to. |
| `version` | Version ID | The label contains the ID of the function version the metric values refer to. |
| `bin` | Interval of histogram values | For metrics represented by a histogram, the label value describes the interval of the measured value during which the event occurred. |
