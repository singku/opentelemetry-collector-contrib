# AlibabaCloud LogService Exporter

<!-- status autogenerated section -->
| Status        |           |
| ------------- |-----------|
| Stability     | [beta]: traces, metrics, logs   |
| Distributions | [contrib] |
| Issues        | [![Open issues](https://img.shields.io/github/issues-search/open-telemetry/opentelemetry-collector-contrib?query=is%3Aissue%20is%3Aopen%20label%3Aexporter%2Falibabacloudlogservice%20&label=open&color=orange&logo=opentelemetry)](https://github.com/open-telemetry/opentelemetry-collector-contrib/issues?q=is%3Aopen+is%3Aissue+label%3Aexporter%2Falibabacloudlogservice) [![Closed issues](https://img.shields.io/github/issues-search/open-telemetry/opentelemetry-collector-contrib?query=is%3Aissue%20is%3Aclosed%20label%3Aexporter%2Falibabacloudlogservice%20&label=closed&color=blue&logo=opentelemetry)](https://github.com/open-telemetry/opentelemetry-collector-contrib/issues?q=is%3Aclosed+is%3Aissue+label%3Aexporter%2Falibabacloudlogservice) |
| Code coverage | [![codecov](https://codecov.io/github/open-telemetry/opentelemetry-collector-contrib/graph/main/badge.svg?component=exporter_alibabacloud_logservice)](https://app.codecov.io/gh/open-telemetry/opentelemetry-collector-contrib/tree/main/?components%5B0%5D=exporter_alibabacloud_logservice&displayType=list) |
| [Code Owners](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/CONTRIBUTING.md#becoming-a-code-owner)    | [@shabicheng](https://www.github.com/shabicheng), [@kongluoxing](https://www.github.com/kongluoxing), [@qiansheng91](https://www.github.com/qiansheng91) |

[beta]: https://github.com/open-telemetry/opentelemetry-collector/blob/main/docs/component-stability.md#beta
[contrib]: https://github.com/open-telemetry/opentelemetry-collector-releases/tree/main/distributions/otelcol-contrib
<!-- end autogenerated section -->

This exporter supports sending OpenTelemetry data to [LogService](https://www.alibabacloud.com/product/log-service).

# Configuration options:

- `endpoint` (required): LogService's [Endpoint](https://www.alibabacloud.com/help/doc-detail/29008.htm).
- `project` (required): LogService's Project Name.
- `logstore` (required): LogService's store Name. For metrics data, you should use metric store.
- `access_key_id` (optional): AlibabaCloud access key id.
- `access_key_secret` (optional): AlibabaCloud access key secret.
- `ecs_ram_role` (optional): set AlibabaCLoud ECS ram role if you are using ACK.
- `token_file_path` (optional): Set token file path if you are using ACK.

# Example:
## Simple Trace Data

```yaml
receivers:
  examplereceiver:

exporters:
  alibabacloud_logservice:
    endpoint: "cn-hangzhou.log.aliyuncs.com"
    project: "demo-project"
    logstore: "traces-store"
    access_key_id: "access-key-id"
    access_key_secret: "access-key-secret"

service:
  pipelines:
    traces:
      receivers: [examplereceiver]
      exporters: [alibabacloud_logservice]
```


## All Telemetry Data
If you are using OpenTelemetry Collector to collect different types of telemetry data, you should send to different LogService's store.

```yaml
receivers:
  examplereceiver:

exporters:
  alibabacloud_logservice/logs:
    endpoint: "cn-hangzhou.log.aliyuncs.com"
    project: "demo-project"
    logstore: "logs-store"
    access_key_id: "access-key-id"
    access_key_secret: "access-key-secret"
  alibabacloud_logservice/metrics:
    endpoint: "cn-hangzhou.log.aliyuncs.com"
    project: "demo-project"
    logstore: "metrics-store"
    access_key_id: "access-key-id"
    access_key_secret: "access-key-secret"
  alibabacloud_logservice/traces:
    endpoint: "cn-hangzhou.log.aliyuncs.com"
    project: "demo-project"
    logstore: "traces-store"
    access_key_id: "access-key-id"
    access_key_secret: "access-key-secret"

service:
  pipelines:
    traces:
      receivers: [examplereceiver]
      exporters: [alibabacloud_logservice/traces]
    logs:
      receivers: [examplereceiver]
      exporters: [alibabacloud_logservice/logs]
    metrics:
      receivers: [examplereceiver]
      exporters: [alibabacloud_logservice/metrics]
```
