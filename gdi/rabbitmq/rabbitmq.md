(rabbitmq)=

# RabbitMQ
<meta name="description" content="Use this Splunk Observability Cloud integration for the RabbitMQ monitor. See benefits, install, configuration, and metrics">

## Description

The {ref}`Splunk Distribution of OpenTelemetry Collector <otel-intro>` provides this integration as the RabbitMQ monitor type using the Smart Agent Receiver.

Use this monitor to keep track of an instance of RabbitMQ by using the RabbitMQ Python Plugin. This monitor uses the RabbitMQ Management HTTP API to poll for statistics on a RabbitMQ server, then reports them to the agent.

This integration is available for Kubernetes, Windows, and Linux.

### Benefits

```{include} /_includes/benefits.md
```

### Requirements

This monitor requires RabbitMQ 3.0 and higher.

## Installation

```{include} /_includes/collector-installation.md
```

## Configuration

```{include} /_includes/configuration.md
```

```{note}
Provide a RabbitMQ monitor entry in your Collector or Smart Agent (deprecated) configuration. Use the appropriate form for your agent type.
```

### Splunk Distribution of OpenTelemetry Collector

To activate this monitor in the Splunk Distribution of OpenTelemetry Collector, add the following to your agent configuration:

```yaml
receivers:
  smartagent/rabbitmq:
    type: collectd/rabbitmq
    ...  # Additional config
```

To complete the monitor activation, you must also include the `smartagent/rabbitmq` receiver item in a `metrics` pipeline. To do this, add the receiver item to the `service` > `pipelines` > `metrics` > `receivers` section of your configuration file. For example:

```yaml
service:
  pipelines:
    metrics:
      receivers: [smartagent/rabbitmq]
```

### Smart Agent

To activate this monitor in the Smart Agent, add the following to your agent configuration:

```yaml
monitors:  # All monitor config goes under this key
  - type: collectd/rabbitmq
    ...  # Additional config
```

See {ref}`smart-agent` for an autogenerated example of a YAML configuration file, with default values where applicable.

### Configuration settings

The following table shows the configuration options for the RabbitMQ monitor:

| Option | Required | Type | Description |
| --- | --- | --- | --- |
| `pythonBinary` | No | `string` | Path to the Python binary. If not set, a built-in runtime is used. This setting can include arguments to the binary. |
| `host` | Yes | `string` | Hostname or IP address of the RabbitMQ instance. For example, `127.0.0.1`. |
| `port` | Yes | `integer` | The port of the RabbitMQ instance. For example, `15672`. |
| `brokerName` | No | `string` | Name of the RabbitMQ instance. Can be a Go template using other configuration options. Used as the `plugin_instance` dimension. The default value is `{{.host}}-{{.port}}`. |
| `collectChannels` | No | `bool` | Whether to collect channels. The default value is`false`. |
| `collectConnections` | No | `bool` |  Whether to collect connections. The default value is`false`. |
| `collectExchanges` | No | `bool` | Whether to collect exchanges. The default value is`false`. |
| `collectNodes` | No | `bool` | Whether to collect nodes. The default value is`false`. |
| `collectQueues` | No | `bool` | Whether to collect queues. The default value is`false`. |
| `httpTimeout` | No | `integer` | HTTP timeout for requests. |
| `verbosityLevel` | No | `string` | Verbosity level. |
| `username` | Yes | `string` | API username of the RabbitMQ instance. |
| `password` | Yes | `string` | API password of the RabbitMQ instance. |
| `useHTTPS` | No | `bool` | Whether to enable HTTPS. The default value is`false`. |
| `sslCACertFile` | No | `string` | Path to the SSL or TLS certificate of the root certificate authority implicitly trusted by this monitor. |
| `sslCertFile` | No | `string` | Path to this monitor's own SSL or TLS certificate. |
| `sslKeyFile` | No | `string` | Path to this monitor's private SSL or TLS key file. |
| `sslKeyPassphrase` | No | `string` | This monitor's private SSL or TLS key file password, if any. |
| `sslVerify` | No | `bool` | Whether the monitor verifies the RabbitMQ Management plugin SSL or TLS certificate. The default value is`false`. |

```{note}
You must enable each of the five `collect*` options to gather metrics pertaining to those facets of a RabbitMQ instance.
```

## Metrics

The following metrics are available for this integration:

<div class="metrics-yaml" url="https://raw.githubusercontent.com/signalfx/integrations/main/rabbitmq/metrics.yaml"></div>

## Get help

```{include} /_includes/troubleshooting.md
```
