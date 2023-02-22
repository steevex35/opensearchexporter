# TCP Receiver

| Status                   |           |
| ------------------------ |-----------|
| Stability                | [alpha]   |
| Supported pipeline types | logs      |
| Distributions            | [contrib] |

Receives logs over TCP.

## Configuration

| Field             | Default          | Description                                                                                                        |
| ---               | ---              | ---                                                                                                                |
| `max_log_size`    | `1MiB`           | The maximum size of a log entry to read before failing. Protects against reading large amounts of data into memory |
| `listen_address`  | required         | A listen address of the form `<ip>:<port>`                                                                         |
| `tls`             | nil              | An optional `TLS` configuration (see the TLS configuration section)                                                |
| `attributes`      | {}               | A map of `key: value` pairs to add to the entry's attributes                                                       |
| `resource`        | {}               | A map of `key: value` pairs to add to the entry's resource                                                         |
| `add_attributes`  | false            | Adds `net.*` attributes according to [semantic convention][https://github.com/open-telemetry/opentelemetry-specification/blob/main/specification/trace/semantic_conventions/span-general.md#general-network-connection-attributes] |
| `multiline`       |                  | A `multiline` configuration block. See below for details                                                           |
| `encoding`        | `utf-8`          | The encoding of the file being read. See the list of supported encodings below for available options               |
| `operators`       | []               | An array of [operators](../../pkg/stanza/docs/operators/README.md#what-operators-are-available). See below for more details |

### TLS Configuration

The `tcplog` receiver supports TLS, disabled by default.
config more detail [opentelemetry-collector#configtls](https://github.com/open-telemetry/opentelemetry-collector/tree/main/config/configtls#tls-configuration-settings).

| Field             | Default          | Description                               |
| ---               | ---              | ---                                       |
| `cert_file`       |                  | Path to the TLS cert to use for TLS required connections.   |
| `key_file`        |                  | Path to the TLS key to use for TLS required connections.       |
| `ca_file`         |                  | Path to the CA cert. For a client this verifies the server certificate. For a server this verifies client certificates. If empty uses system root CA.        |
| `client_ca_file`  |                  | Path to the TLS cert to use by the server to verify a client certificate. (optional)   |

### Operators

Each operator performs a simple responsibility, such as parsing a timestamp or JSON. Chain together operators to process logs into a desired format.

- Every operator has a `type`.
- Every operator can be given a unique `id`. If you use the same type of operator more than once in a pipeline, you must specify an `id`. Otherwise, the `id` defaults to the value of `type`.
- Operators will output to the next operator in the pipeline. The last operator in the pipeline will emit from the receiver. Optionally, the `output` parameter can be used to specify the `id` of another operator to which logs will be passed directly.
- Only parsers and general purpose operators should be used.

### Parsers with Embedded Operations

Many parsers operators can be configured to embed certain followup operations such as timestamp and severity parsing. For more information, see [complex parsers](../../pkg/stanza/docs/types/parsers.md#complex-parsers).

#### `multiline` configuration

If set, the `multiline` configuration block instructs the `tcplog` receiver to split log entries on a pattern other than newlines.

The `multiline` configuration block must contain exactly one of `line_start_pattern` or `line_end_pattern`. These are regex patterns that
match either the beginning of a new log entry, or the end of a log entry.

#### Supported encodings

| Key        | Description
| ---        | ---                                                              |
| `nop`      | No encoding validation. Treats the file as a stream of raw bytes |
| `utf-8`    | UTF-8 encoding                                                   |
| `utf-16le` | UTF-16 encoding with little-endian byte order                    |
| `utf-16be` | UTF-16 encoding with little-endian byte order                    |
| `ascii`    | ASCII encoding                                                   |
| `big5`     | The Big5 Chinese character encoding                              |

Other less common encodings are supported on a best-effort basis.
See [https://www.iana.org/assignments/character-sets/character-sets.xhtml](https://www.iana.org/assignments/character-sets/character-sets.xhtml)
for other encodings available.

## Example Configurations

### Simple

Configuration:

```yaml
receivers:
  tcplog:
    listen_address: "0.0.0.0:54525"
```
[alpha]:https://github.com/open-telemetry/opentelemetry-collector#alpha
[contrib]:https://github.com/open-telemetry/opentelemetry-collector-releases/tree/main/distributions/otelcol-contrib