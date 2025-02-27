(solr)=

# SolrCloud
<meta name="description" content="Use this Splunk Observability Cloud integration for the SolrCloud monitor. See benefits, install, configuration, and metrics">

## Description

The {ref}`Splunk Distribution of OpenTelemetry Collector <otel-intro>` provides this integration as the SolrCloud monitor type using the Smart Agent receiver.

Use this integration to monitor Solr instances. You can collect metrics only when the instance is running in SolrCloud mode.

This integration is available for Kubernetes, Windows, and Linux.

## Benefits

```{include} /_includes/benefits.md
```

## Installation

```{include} /_includes/collector-installation.md
```

## Configuration

```{include} /_includes/configuration.md
```

```{note}
Provide a SolrCloud monitor entry in your Collector or Smart Agent (deprecated) configuration. Use the appropriate form for your agent type.
```

### Splunk Distribution of OpenTelemetry Collector

To activate this monitor in the Splunk Distribution of OpenTelemetry Collector, add the following to your agent configuration:

```yaml 
receivers:
  smartagent/solr:
    type: collectd/solr
    ...  # Additional config
```

To complete the monitor activation, you must also include the `smartagent/solr` receiver item in a `metrics` pipeline. To do this, add the receiver item to the `service` > `pipelines` > `metrics` > `receivers` section of your configuration file. For example:

```yaml
service:
  pipelines:
    metrics:
      receivers: [smartagent/solr]
```

### Smart Agent

To activate this monitor in the Smart Agent, add the following to your agent configuration:

```yaml
monitors:  # All monitor config goes under this key
  - type: collectd/solr
    ...  # Additional config
```

See {ref}`smart-agent` for an autogenerated example of a YAML configuration file, with default values where applicable.

### Configuration settings

The following table shows the configuration options for this monitor:

| Option | Required | Type | Description |
| --- | --- | --- | --- |
| `pythonBinary` | No | `string` | Path to the Python binary. If not set, a built-in runtime is used. Can include arguments to the binary. |
| `host` | Yes | `string` | Host or address of the Solr instance. For example, `127.0.0.1`. |
| `port` | Yes | `integer` | Port of the Solr instance. |
| `cluster` | No | `string` | Name of the Solr cluster. |
| `enhancedMetrics` | No | `bool` | Whether stats from the `/metrics` endpoint are needed. The default value is`false`. |
| `includeMetrics` | No | `list of strings` | List of metric names from the `/admin/metrics` endpoint to include. Valid when `EnhancedMetrics` is "false". |
| `excludeMetrics` | No | `list of strings` | List of metric names from the `/admin/metrics` endpoint to exclude. Valid when `EnhancedMetrics` is "true". |

## Metrics

These metrics are available for this integration:

<div class="metrics-yaml" url="https://raw.githubusercontent.com/signalfx/signalfx-agent/main/pkg/monitors/collectd/solr/metadata.yaml"></div>

## Get help

```{include} /_includes/troubleshooting.md
```
