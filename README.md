# prometheus-webhook-dingtalk

Generating [DingTalk] notification from [Prometheus] [AlertManager] WebHooks.

## Building and running

### Build

```bash
make
```

### Running

```bash
./prometheus-webhook-dingtalk <flags>
```

## Usage

```
usage: prometheus-webhook-dingtalk [<flags>]

Flags:
  -h, --help               Show context-sensitive help (also try --help-long and --help-man).
      --web.listen-address=:8060
                           The address to listen on for web interface.
      --config.file=config.yml
                           Path to the configuration file.
      --log.level=info     Only log messages with the given severity or above. One of: [debug, info, warn, error]
      --log.format=logfmt  Output format of log messages. One of: [logfmt, json]
      --version            Show application version.

```

## Configuration

常见问题可以看看 [FAQ](./docs/FAQ_zh.md)

```yaml
## Request timeout
# timeout: 5s

## Customizable templates path
templates:
  - templates/cutomization.tmpl

## Targets, previously was known as "profiles"
targets:
  webhook1:
    url: https://oapi.dingtalk.com/robot/send?access_token=xxxxxxxxxxxx
    # secret for signature
    secret: SEC000000000000000000000
  webhook2:
    url: https://oapi.dingtalk.com/robot/send?access_token=xxxxxxxxxxxx
  webhook_legacy:
    url: https://oapi.dingtalk.com/robot/send?access_token=xxxxxxxxxxxx
    # Customize template content
    message:
      # Use legacy template
      title: '{{ template "legacy.title" . }}'
      text: '{{ template "legacy.text" . }}'
  webhook_mention_all:
    url: https://oapi.dingtalk.com/robot/send?access_token=xxxxxxxxxxxx
    mention:
      all: true
  webhook_mention_users:
    mention:
      mobiles: ['156xxxx8827', '189xxxx8325']
```

## Using Docker

You can deploy this tool using the Docker image from following registry:

* [DockerHub]\: [timonwong/prometheus-webhook-dingtalk](https://hub.docker.com/r/timonwong/prometheus-webhook-dingtalk)
* [Quay.io]\:
  * [timonwong/prometheus-webhook-dingtalk-linux-amd64](https://quay.io/repository/timonwong/prometheus-webhook-dingtalk-linux-amd64)
  * [timonwong/prometheus-webhook-dingtalk-linux-armv7](https://quay.io/repository/timonwong/prometheus-webhook-dingtalk-linux-armv7)
  * [timonwong/prometheus-webhook-dingtalk-linux-arm64](https://quay.io/repository/timonwong/prometheus-webhook-dingtalk-linux-arm64)

[Prometheus]: https://prometheus.io
[AlertManager]: https://github.com/prometheus/alertmanager
[DingTalk]: https://www.dingtalk.com
[DockerHub]: https://hub.docker.com
[Quay.io]: https://quay.io
