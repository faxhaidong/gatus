<!-- 本文件由 README.md 翻译生成。代码块、配置键、URL 与原始锚点尽量保持不变。 -->

[![Gatus](.github/assets/logo-with-dark-text.png)](https://gatus.io)

![测试](https://github.com/TwiN/gatus/actions/workflows/test.yml/badge.svg)
[![Go Report Card](https://goreportcard.com/badge/github.com/TwiN/gatus?)](https://goreportcard.com/report/github.com/TwiN/gatus)
[![codecov](https://codecov.io/gh/TwiN/gatus/branch/master/graph/badge.svg)](https://codecov.io/gh/TwiN/gatus)
[![Go版本](https://img.shields.io/github/go-mod/go-version/TwiN/gatus.svg)](https://github.com/TwiN/gatus)
[![Docker 拉取](https://img.shields.io/docker/pulls/twinproduction/gatus.svg)](https://cloud.docker.com/repository/docker/twinproduction/gatus)
[![关注 TwiN](https://img.shields.io/github/followers/TwiN?label=Follow&style=social)](https://github.com/TwiN)

Gatus 是一个面向开发人员的健康仪表板，使您能够使用 HTTP、ICMP、TCP 甚至 DNS 监控您的服务
查询以及通过使用状态代码等值的条件列表来评估所述查询的结果，
响应时间、证书过期、正文等等。最重要的是，这些健康
检查可以与通过 Slack、Teams、PagerDuty、Discord、Twilio 等发出的告警配对。

我亲自将它部署在我的 Kubernetes 集群中并让它监控我的状态
核心应用：https://status.twin.sh/

_正在寻找托管解决方案？查看 [Gatus.io](https://gatus.io)._

<details>
  <summary><b>快速开始</b></summary>

```console
docker run -p 8080:8080 --name gatus ghcr.io/twin/gatus:stable
```

如果您愿意，还可以使用 Docker Hub：
```console
docker run -p 8080:8080 --name gatus twinproduction/gatus:stable
```
更多详情请参见【使用方法】(#usage)
</details>

> ❤ 喜欢这个项目吗？请考虑[赞助我](https://github.com/sponsors/TwiN)。

![Gatus 仪表板](.github/assets/dashboard-dark.jpg)

有任何反馈或问题吗？ [创建讨论](https://github.com/TwiN/gatus/discussions/new)。


<a id="table-of-contents"></a>
## 目录
- [目录](#table-of-contents)
- [为什么选择 Gatus？](#why-gatus)
- [特点](#features)
- [使用方法](#usage)
- [配置](#configuration)
  - [端点](#endpoints)
  - [外部端点](#external-endpoints)
  - [套房（ALPHA）](#suites-alpha)
  - [条件](#conditions)
    - [占位符](#placeholders)
    - [功能](#functions)
  - [网页](#web)
  - [UI](#ui)
  - [公告](#announcements)
  - [存储](#storage)
  - [客户端配置](#client-configuration)
  - [隧道](#tunneling)
  - [告警](#alerting)
    - [配置 AWS SES 告警](#configuring-aws-ses-alerts)
    - [配置ClickUp 告警](#configuring-clickup-alerts)
    - [配置Datadog告警](#configuring-datadog-alerts)
    - [配置Discord 告警](#configuring-discord-alerts)
    - [配置电子邮件告警](#configuring-email-alerts)
    - [配置 Gitea 告警](#configuring-gitea-alerts)
    - [配置 GitHub 告警](#configuring-github-alerts)
    - [配置 GitLab 告警](#configuring-gitlab-alerts)
    - [配置 Google Chat提醒](#configuring-google-chat-alerts)
    - [配置 Gotify 告警](#configuring-gotify-alerts)
    - [配置 HomeAssistant 告警](#configuring-homeassistant-alerts)
    - [配置 IFTTT 告警](#configuring-ifttt-alerts)
    - [配置Ilert告警](#configuring-ilert-alerts)
    - [配置 Incident.io 告警](#configuring-incidentio-alerts)
    - [配置Line 告警](#configuring-line-alerts)
    - [配置Matrix 告警](#configuring-matrix-alerts)
    - [配置 Mattermost 告警](#configuring-mattermost-alerts)
    - [配置Messagebird告警](#configuring-messagebird-alerts)
    - [配置 n8n 告警](#configuring-n8n-alerts)
    - [配置New Relic告警](#configuring-new-relic-alerts)
    - [配置 NTFy 告警](#configuring-ntfy-alerts)
    - [配置 Opsgenie 告警](#configuring-opsgenie-alerts)
    - [配置 PagerDuty 告警](#configuring-pagerduty-alerts)
    - [配置 Plivo 告警](#configuring-plivo-alerts)
    - [配置 Pushover 告警](#configuring-pushover-alerts)
    - [配置 Rocket.Chat 提醒](#configuring-rocketchat-alerts)
    - [配置SendGrid告警](#configuring-sendgrid-alerts)
    - [配置Signal 告警](#configuring-signal-alerts)
    - [配置 SIGNL4 告警](#configuring-signl4-alerts)
    - [配置 Slack 告警](#configuring-slack-alerts)
    - [配置 Splunk 告警](#configuring-splunk-alerts)
    - [配置 Squadcast 告警](#configuring-squadcast-alerts)
    - [配置 Teams 告警 *（已弃用）*](#configuring-teams-alerts-deprecated)
    - [配置 Teams 工作流告警](#configuring-teams-workflow-alerts)
    - [配置Telegram 告警](#configuring-telegram-alerts)
    - [配置 Twilio 告警](#configuring-twilio-alerts)
    - [配置 Vonage 告警](#configuring-vonage-alerts)
    - [配置 Webex 告警](#configuring-webex-alerts)
    - [配置 Zapier 告警](#configuring-zapier-alerts)
    - [配置 Zulip 告警](#configuring-zulip-alerts)
    - [配置自定义告警](#configuring-custom-alerts)
    - [设置默认告警](#setting-a-default-alert)
  - [维护](#maintenance)
  - [安全](#security)
    - [基本认证](#basic-authentication)
    - [OIDC](#oidc)
  - [TLS 加密](#tls-encryption)
  - [指标](#metrics)
    - [自定义标签](#custom-labels)
  - [连接](#connectivity)
  - [远程实例（实验）](#remote-instances-experimental)
- [部署](#deployment)
  - [Docker](#docker)
  - [Helm Chart](#helm-chart)
  - [Terraform](#terraform)
    - [Kubernetes](#kubernetes)
- [运行测试](#running-the-tests)
- [生产中使用](#using-in-production)
- [FAQ](#faq)
  - [发送 GraphQL 请求](#sending-a-graphql-request)
  - [推荐间隔](#recommended-interval)
  - [默认超时](#default-timeouts)
  - [监控 TCP 端点](#monitoring-a-tcp-endpoint)
  - [监控UDP端点](#monitoring-a-udp-endpoint)
  - [监控 SCTP 端点](#monitoring-a-sctp-endpoint)
  - [监控 WebSocket 端点](#monitoring-a-websocket-endpoint)
  - [使用 gRPC 监控端点](#monitoring-an-endpoint-using-grpc)
  - [使用 ICMP 监控端点](#monitoring-an-endpoint-using-icmp)
  - [使用 DNS 查询监控端点](#monitoring-an-endpoint-using-dns-queries)
  - [使用 SSH 监控端点](#monitoring-an-endpoint-using-ssh)
  - [使用 STARTTLS 监控端点](#monitoring-an-endpoint-using-starttls)
  - [使用 TLS 监控端点](#monitoring-an-endpoint-using-tls)
  - [监控域名过期](#monitoring-domain-expiration)
  - [并发](#concurrency)
  - [动态重新加载配置](#reloading-configuration-on-the-fly)
  - [端点组](#endpoint-groups)
  - [如何默认按组排序？](#how-do-i-sort-by-group-by-default)
  - [在自定义路径上公开 Gatus](#exposing-gatus-on-a-custom-path)
  - [在自定义端口上公开 Gatus](#exposing-gatus-on-a-custom-port)
  - [在配置文件中使用环境变量](#use-environment-variables-in-config-files)
  - [配置启动延迟](#configuring-a-startup-delay)
  - [保持较小的配置](#keeping-your-configuration-small)
  - [代理客户端配置](#proxy-client-configuration)
  - [如何修复 431 请求标头字段太大错误](#how-to-fix-431-request-header-fields-too-large-error)
  - [徽章](#badges)
    - [正常运行时间](#uptime)
    - [健康](#health)
    - [健康 (Shields.io)](#health-shieldsio)
    - [响应时间](#response-time)
    - [响应时间（图表）](#response-time-chart)
      - [如何更改响应时间徽章的颜色阈值](#how-to-change-the-color-thresholds-of-the-response-time-badge)
  - [API](#api)
    - [以编程方式与 API 交互](#interacting-with-the-api-programmatically)
    - [原始数据](#raw-data)
      - [正常运行时间](#uptime-1)
      - [响应时间](#response-time-1)
  - [作为二进制安装](#installing-as-binary)
  - [高级设计概述](#high-level-design-overview)


<a id="why-gatus"></a>
## 为什么是加图斯？
在讨论具体细节之前，我想先解决一个最常见的问题：
> 当我只能使用 Prometheus 的 Alertmanager、Cloudwatch 甚至 Splunk 时，为什么还要使用 Gatus？

如果没有客户端主动调用端点，这些都不能告诉您存在问题。
换句话说，这是因为监控指标主要依赖于现有流量，这实际上意味着除非
您的客户已经遇到问题，您不会收到通知。

另一方面，Gatus 允许您为每个功能配置运行状况检查，从而允许它
监视这些功能并可能在任何客户端受到影响之前向您发出告警。

您可能想要研究 Gatus 的一个迹象是，只需询问自己，如果您的负载均衡器是否会收到告警
是现在就下去。您现有的告警会被触发吗？您的指标不会报告错误增加
如果没有流量到达您的应用程序。这使您处于这样一种情况：您的客户就是您的客户
这会通知您服务质量下降，而不是让他们放心您正在努力
在他们知道之前解决问题。


<a id="features"></a>
## 功能
Gatus的主要特点是：

- **高度灵活的运行状况检查条件**：虽然检查响应状态对于某些用例来说可能就足够了，但 Gatus 更进一步，允许您添加有关响应时间、响应正文甚至 IP 地址的条件。
- **能够使用 Gatus 进行用户验收测试**：由于上述几点，您可以利用此应用程序来创建自动化的用户验收测试。
- **非常容易配置**：配置不仅设计得尽可能可读，而且添加新服务或新端点进行监控也非常容易。
- **告警**：虽然拥有漂亮的可视化仪表板对于跟踪应用程序的状态很有用，但您可能不想整天盯着它。因此，开箱即用地支持通过 Slack、Mattermost、Messagebird、PagerDuty、Twilio、Google Chat和 Teams 发出的通知，并且能够根据您可能有的任何需求配置自定义告警提供程序，无论是不同的提供程序还是管理自动回滚的自定义应用程序。
- **指标**
- **资源消耗低**：与大多数 Go 应用程序一样，该应用程序所需的资源占用非常小，可以忽略不计。
- **[徽章](#badges)**: ![正常运行时间 7d](https://status.twin.sh/api/v1/endpoints/core_blog-external/uptimes/7d/badge.svg) ![响应时间 24 小时](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/24h/badge.svg)
- **深色模式**

![Gatus 仪表板条件](.github/assets/dashboard-conditions.jpg)


<a id="usage"></a>
## 使用方法

```console
docker run -p 8080:8080 --name gatus ghcr.io/twin/gatus:stable
```

如果您愿意，还可以使用 Docker Hub：
```console
docker run -p 8080:8080 --name gatus twinproduction/gatus:stable
```
如果您想创建自己的配置，请参阅 [Docker](#docker) 了解如何挂载配置文件的信息。

这是一个简单的例子：
```yaml
endpoints:
  - name: website                 # Name of your endpoint, can be anything
    url: "https://twin.sh/health"
    interval: 5m                  # Duration to wait between every status check (default: 60s)
    conditions:
      - "[STATUS] == 200"         # Status must be 200
      - "[BODY].status == UP"     # The json path "$.status" must be equal to UP
      - "[RESPONSE_TIME] < 300"   # Response time must be under 300ms

  - name: make-sure-header-is-rendered
    url: "https://example.org/"
    interval: 60s
    conditions:
      - "[STATUS] == 200"                          # Status must be 200
      - "[BODY] == pat(*<h1>Example Domain</h1>*)" # Body must contain the specified header
```

这个例子看起来类似于：

![简单示例](.github/assets/example.jpg)

如果您想在本地测试，请参阅[Docker](#docker)。

<a id="configuration"></a>
## 配置
默认情况下，配置文件应位于 `config/config.yaml`。

您可以通过设置 `GATUS_CONFIG_PATH` 环境变量来指定自定义路径。

如果 `GATUS_CONFIG_PATH` 指向一个目录，则该目录及其目录中的所有 `*.yaml` 和 `*.yml` 文件
子目录合并如下：
- 所有地图/对象均深度合并（即您可以在一个文件中定义 `alerting.slack`，在另一个文件中定义 `alerting.pagerduty`）
- 所有切片/数组都被附加（即您可以在多个文件中定义 `endpoints`，每个端点将被添加到最终的端点列表中）
- 具有原始值的参数（例如 `metrics`、`alerting.slack.webhook-url` 等）只能定义一次，以强制避免任何歧义
    - To clarify, this also means that you could not define `alerting.slack.webhook-url` in two files with different values.所有文件在处理之前都会合并为一个。这是设计使然。

> 💡 您还可以在配置文件中使用环境变量（例如 `$DOMAIN`、`${DOMAIN}`）
>
> ⚠️ 当您的配置参数包含 `$` 符号时，您必须使用 `$$` 转义 `$`。
>
> 有关示例，请参阅 [在配置文件中使用环境变量](#use-environment-variables-in-config-files) 或 [examples/docker-compose-postgres-storage/config/config.yaml](.examples/docker-compose-postgres-storage/config/config.yaml)。

如果您想在本地测试，请参阅[Docker](#docker)。


<a id="configuration"></a>
## 配置
|范围|描述|默认|
|:-----------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|:--------------|
|`metrics`|是否公开 `/metrics` 处的指标。|`false`|
|`storage`|[存储配置](#storage)。|`{}`|
|`alerting`|[告警配置](#alerting)。|`{}`|
|`announcements`|[公告配置](#announcements)。|`[]`|
|`endpoints`|[端点配置](#endpoints)。|必需 `[]`|
|`external-endpoints`|[外部端点配置](#external-endpoints)。|`[]`|
|`security`|[安全配置](#security)。|`{}`|
|`concurrency`|同时监控的端点/套件的最大数量。设置为 `0` 表示无限制。请参阅[并发](#concurrency)。|`3`|
|`disable-monitoring-lock`|是否[禁用监控锁](#disable-monitoring-lock)。 **已弃用**：使用 `concurrency: 0` 代替。|`false`|
|`skip-invalid-config-update`|是否忽略无效的配置更新。 <br />请参见[动态重新加载配置](#reloading-configuration-on-the-fly)。|`false`|
|`web`|[网页配置](#web)。|`{}`|
|`ui`|[UI配置](#ui)。|`{}`|
|`maintenance`|[维护配置](#maintenance)。|`{}`|

如果您想要更详细的日志记录，可以将 `GATUS_LOG_LEVEL` 环境变量设置为 `DEBUG`。
相反，如果您想要较少的详细日志记录，可以将上述环境变量设置为 `WARN`、`ERROR` 或 `FATAL`。
`GATUS_LOG_LEVEL` 的默认值为 `INFO`。

<a id="endpoints"></a>
### 端点
端点是您要监控的 URL、应用程序或服务。每个端点都有一个条件列表，这些条件是
根据您定义的时间间隔进行评估。如果任何条件失败，端点将被视为不健康。
然后，您可以将告警配置为在端点不健康且达到特定阈值时触发。

|范围|描述|默认|
|:------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------|
|`endpoints`|要监视的端点列表。|必需 `[]`|
|`endpoints[].enabled`|是否监控端点。|`true`|
|`endpoints[].name`|端点的名称。可以是任何东西。|必需 `""`|
|`endpoints[].group`|团体名称。用于在仪表板上将多个端点分组在一起。 <br />请参阅[端点组](#endpoint-groups)。|`""`|
|`endpoints[].url`|将请求发送到的 URL。|必需 `""`|
|`endpoints[].method`|请求方法。|`GET`|
|`endpoints[].conditions`|用于确定端点运行状况的条件。 <br />参见[条件](#conditions)。|`[]`|
|`endpoints[].interval`|每次状态检查之间等待的时间。|`60s`|
|`endpoints[].graphql`|是否将正文包装在查询参数中 (`{"query":"$body"}`)。|`false`|
|`endpoints[].body`|请求正文。|`""`|
|`endpoints[].headers`|请求标头。|`{}`|
|`endpoints[].dns`|DNS 类型端点的配置。 <br />请参阅[使用 DNS 查询监控端点](#monitoring-an-endpoint-using-dns-queries)。|`""`|
|`endpoints[].dns.query-type`|查询类型（例如 MX）。|`""`|
|`endpoints[].dns.query-name`|查询名称（例如 example.com）。|`""`|
|`endpoints[].ssh`|SSH 类型端点的配置。 <br />请参阅[使用 SSH 监控端点](#monitoring-an-endpoint-using-ssh)。|`""`|
|`endpoints[].ssh.username`|SSH 用户名（例如示例）。|必需 `""`|
|`endpoints[].ssh.password`|SSH 密码（例如密码）。|必需 `""`|
|`endpoints[].alerts`|给定端点的所有告警的列表。 <br />请参阅[告警](#alerting)。|`[]`|
|`endpoints[].maintenance-windows`|给定端点的所有维护时段的列表。 <br />参见[维护](#maintenance)。|`[]`|
|`endpoints[].client`|[客户端配置](#client-configuration)。|`{}`|
|`endpoints[].ui`|端点级别的 UI 配置。|`{}`|
|`endpoints[].ui.hide-conditions`|是否从结果中隐藏条件。请注意，这只会隐藏启用此功能后评估的结果中的条件。|`false`|
|`endpoints[].ui.hide-hostname`|是否在结果中隐藏主机名。|`false`|
|`endpoints[].ui.hide-port`|是否在结果中隐藏端口。|`false`|
|`endpoints[].ui.hide-url`|是否在结果中隐藏 URL。如果 URL 包含令牌，则很有用。|`false`|
|`endpoints[].ui.hide-errors`|是否隐藏结果中的错误。|`false`|
|`endpoints[].ui.dont-resolve-failed-conditions`|是否解决 UI 的失败条件。|`false`|
|`endpoints[].ui.resolve-successful-conditions`|是否解决 UI 的成功条件（即使检查通过也有助于公开主体断言）。|`false`|
|`endpoints[].ui.badge.response-time`|响应时间阈值列表。每次达到阈值时，徽章都会有不同的颜色。|`[50, 200, 300, 500, 750]`|
|`endpoints[].extra-labels`|添加到指标的额外标签。对于将端点分组在一起很有用。|`{}`|
|`endpoints[].always-run`|（仅限套件）即使套件中的先前端点失败，是否也执行此端点。|`false`|
|`endpoints[].store`|（仅限套件）从响应中提取并存储在套件上下文中的值映射（即使出现故障也存储）。|`{}`|

您可以在正文中使用以下占位符 (`endpoints[].body`)：
- `[ENDPOINT_NAME]`（从 `endpoints[].name` 解析）
- `[ENDPOINT_GROUP]`（从 `endpoints[].group` 解析）
- `[ENDPOINT_URL]`（从 `endpoints[].url` 解析）
- `[LOCAL_ADDRESS]`（解析为本地 IP 和端口，如 `192.0.2.1:25` 或 `[2001:db8::1]:80`）
- `[RANDOM_STRING_N]`（解析为长度为 N 的数字和字母的随机字符串（最大：8192））

<a id="external-endpoints"></a>
### 外部端点
与常规端点不同，外部端点不受 Gatus 监控，而是以编程方式推送。
这使您可以监视您想要监视的任何内容，即使您想要检查的内容位于 Gatus 通常无法访问的环境中。

例如：
- 您可以创建自己的代理，该代理位于专用网络中，并将服务的状态推送到公开的 Gatus 实例
- 您可以监控 Gatus 不支持的服务
- 您可以使用Gatus作为仪表板来实现自己的监控系统

|范围|描述|默认|
|:------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------|:---------------|
|`external-endpoints`|要监视的端点列表。|`[]`|
|`external-endpoints[].enabled`|是否监控端点。|`true`|
|`external-endpoints[].name`|端点的名称。可以是任何东西。|必需 `""`|
|`external-endpoints[].group`|团体名称。用于在仪表板上将多个端点分组在一起。 <br />请参阅[端点组](#endpoint-groups)。|`""`|
|`external-endpoints[].token`|需要持有者令牌才能将状态推送到。|必需 `""`|
|`external-endpoints[].alerts`|给定端点的所有告警的列表。 <br />请参阅[告警](#alerting)。|`[]`|
|`external-endpoints[].heartbeat`|用于监视外部端点何时停止发送更新的心跳配置。|`{}`|
|`external-endpoints[].heartbeat.interval`|预期的更新间隔。如果在此时间间隔内未收到更新，则会触发告警。必须至少 10 秒。|`0`（已禁用）|

例子：
```yaml
external-endpoints:
  - name: ext-ep-test
    group: core
    token: "potato"
    heartbeat:
      interval: 30m  # Automatically create a failure if no update is received within 30 minutes
    alerts:
      - type: discord
        description: "healthcheck failed"
        send-on-resolved: true
```

要推送外部端点的状态，您可以使用 [gatus-cli](https://github.com/TwiN/gatus-cli)：
```
gatus-cli external-endpoint push --url https://status.example.org --key "core_ext-ep-test" --token "potato" --success
```

或发送 HTTP 请求：
```
POST /api/v1/endpoints/{key}/external?success={success}&error={error}&duration={duration}
```
在哪里：
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。
  - 使用上面的示例配置，密钥将为 `core_ext-ep-test`。
- `{success}` 是一个布尔值（`true` 或 `false`），指示运行状况检查是否成功。
- `{error}`（可选）：描述健康检查失败原因的字符串。如果 {success} 为 false，则应包含错误消息；如果检查成功，这将被忽略。
- `{duration}`（可选）：请求作为持续时间字符串所花费的时间（例如 10 秒）。

您还必须在 `Authorization` 标头中将令牌作为 `Bearer` 令牌传递。


<a id="suites-alpha"></a>
### 套房（阿尔法）
套件是使用共享上下文顺序执行的端点的集合。
这允许您创建复杂的监控场景，其中一个端点的结果可以在后续端点中使用，从而实现工作流式监控。

以下是套件可能有用的几种情况：
- 测试多步骤身份验证流程（登录 -> 访问受保护资源 -> 注销）
- 您需要链接请求的 API 工作流程（创建资源 -> 更新 -> 验证 -> 删除）
- 监控跨多个服务的业务流程
- 验证多个端点之间的数据一致性

|范围|描述|默认|
|:----------------------------------|:----------------------------------------------------------------------------------------------------|:--------------|
|`suites`|要监视的套件列表。|`[]`|
|`suites[].enabled`|是否监控套件。|`true`|
|`suites[].name`|套房的名称。必须是独一无二的。|必需 `""`|
|`suites[].group`|团体名称。用于在仪表板上将多个套件分组在一起。|`""`|
|`suites[].interval`|套件执行之间等待的持续时间。|`10m`|
|`suites[].timeout`|整个套件执行的最大持续时间。|`5m`|
|`suites[].context`|端点可以引用的初始上下文值。|`{}`|
|`suites[].endpoints`|要顺序执行的端点列表。|必需 `[]`|
|`suites[].endpoints[].store`|从响应中提取并存储在套件上下文中的值映射（即使在失败时也存储）。|`{}`|
|`suites[].endpoints[].always-run`|即使套件中的先前端点失败，是否也执行此端点。|`false`|

**注意**：尚不支持套件级别告警。相反，在套件内的各个端点上配置告警。

<a id="using-context-in-endpoints"></a>
#### 在端点中使用上下文
一旦值存储在上下文中，就可以在后续端点中引用它们：
- 在网址中：`https://api.example.com/users/[CONTEXT].user_id`
- 在标题中：`Authorization: Bearer [CONTEXT].auth_token`
- 体内：`{"user_id": "[CONTEXT].user_id"}`
- 条件：`[BODY].server_ip == [CONTEXT].server_ip`

请注意，上下文/存储键仅限于 A-Z、a-z、0-9、下划线 (`_`) 和连字符 (`-`)。

<a id="example-suite-configuration"></a>
#### 套件配置示例
```yaml
suites:
  - name: item-crud-workflow
    group: api-tests
    interval: 5m
    context:
      price: "19.99"  # Initial static value in context
    endpoints:
      # Step 1: Create an item and store the item ID
      - name: create-item
        url: https://api.example.com/items
        method: POST
        body: '{"name": "Test Item", "price": "[CONTEXT].price"}'
        conditions:
          - "[STATUS] == 201"
          - "len([BODY].id) > 0"
          - "[BODY].price == [CONTEXT].price"
        store:
          itemId: "[BODY].id"
        alerts:
          - type: slack
            description: "Failed to create item"

      # Step 2: Update the item using the stored item ID
      - name: update-item
        url: https://api.example.com/items/[CONTEXT].itemId
        method: PUT
        body: '{"price": "24.99"}'
        conditions:
          - "[STATUS] == 200"
        alerts:
          - type: slack
            description: "Failed to update item"

      # Step 3: Fetch the item and validate the price
      - name: get-item
        url: https://api.example.com/items/[CONTEXT].itemId
        method: GET
        conditions:
          - "[STATUS] == 200"
          - "[BODY].price == 24.99"
        alerts:
          - type: slack
            description: "Item price did not update correctly"

      # Step 4: Delete the item (always-run: true to ensure cleanup even if step 2 or 3 fails)
      - name: delete-item
        url: https://api.example.com/items/[CONTEXT].itemId
        method: DELETE
        always-run: true
        conditions:
          - "[STATUS] == 204"
        alerts:
          - type: slack
            description: "Failed to delete item"
```

仅当所有必需的端点都通过其条件时，该套件才会被视为成功。


<a id="conditions"></a>
### 状况
以下是您可以使用的一些条件示例：

|健康）状况|描述|传递值|失败的价值观|
|:---------------------------------|:----------------------------------------------------|:---------------------------|------------------|
|`[STATUS] == 200`|状态必须等于 200|200|201、404、...|
|`[STATUS] < 300`|状态必须低于 300|200、201、299|301、302、……|
|`[STATUS] <= 299`|状态必须小于或等于 299|200、201、299|301、302、……|
|`[STATUS] > 400`|状态必须大于 400|401、402、403、404|400、200、...|
|`[STATUS] == any(200, 429)`|状态必须为 200 或 429|200, 429|201、400、...|
|`[CONNECTED] == true`|与主机的连接必须已成功|真的|错误的|
|`[RESPONSE_TIME] < 500`|响应时间必须低于 500ms|100毫秒、200毫秒、300毫秒|500毫秒、501毫秒|
|`[IP] == 127.0.0.1`|目标IP必须是127.0.0.1|127.0.0.1|0.0.0.0|
|`[BODY] == 1`|主体必须等于 1|1|`{}`、`2`、...|
|`[BODY].user.name == john`|`$.user.name` 的 JSONPath 值等于 `john`|`{"user":{"name":"john"}}`|                  |
|`[BODY].data[0].id == 1`|`$.data[0].id` 的 JSONPath 值等于 1|`{"data":[{"id":1}]}`|                  |
|`[BODY].age == [BODY].id`|`$.age` 的 JSONPath 值等于 JSONPath `$.id`|`{"age":1,"id":1}`|                  |
|`len([BODY].data) < 5`|JSONPath `$.data` 处的数组少于 5 个元素|`{"data":[{"id":1}]}`|                  |
|`len([BODY].name) == 8`|JSONPath `$.name` 处的字符串长度为 8|`{"name":"john.doe"}`|`{"name":"bob"}`|
|`has([BODY].errors) == false`|JSONPath `$.errors` 不存在|`{"name":"john.doe"}`|`{"errors":[]}`|
|`has([BODY].users) == true`|JSONPath `$.users` 存在|`{"users":[]}`|`{}`|
|`[BODY].name == pat(john*)`|JSONPath `$.name` 处的字符串与模式 `john*` 匹配|`{"name":"john.doe"}`|`{"name":"bob"}`|
|`[BODY].id == any(1, 2)`|JSONPath `$.id` 的值等于 `1` 或 `2`|1, 2|3, 4, 5|
|`[CERTIFICATE_EXPIRATION] > 48h`|距离证书到期还有 48 小时以上|49小时、50小时、123小时|1小时、24小时、...|
|`[DOMAIN_EXPIRATION] > 720h`|域名必须在 720 小时内过期|4000小时|1小时、24小时、...|


<a id="placeholders"></a>
#### 占位符
|占位符|描述|解析值示例|
|:---------------------------|:------------------------------------------------------------------------------------------|:---------------------------------------------|
|`[STATUS]`|解析为请求的 HTTP 状态|`404`|
|`[RESPONSE_TIME]`|解析为请求所花费的响应时间（以毫秒为单位）|`10`|
|`[IP]`|解析为目标主机的IP|`192.168.0.232`|
|`[BODY]`|解析为响应正文。支持 JSONPath。|`{"name":"john.doe"}`|
|`[CONNECTED]`|解析是否可以建立连接|`true`|
|`[CERTIFICATE_EXPIRATION]`|解析为证书过期之前的持续时间（有效单位为“s”、“m”、“h”。）|`24h`、`48h`、0（如果没有带证书的协议）|
|`[DOMAIN_EXPIRATION]`|解析为域过期之前的持续时间（有效单位为“s”、“m”、“h”。）|`24h`、`48h`、`1234h56m78s`|
|`[DNS_RCODE]`|解析为响应的 DNS 状态|`NOERROR`|


<a id="functions"></a>
#### 功能
|功能|描述|例子|
|:---------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------|
|`len`|如果给定路径通向数组，则返回其长度。否则，给定路径处的 JSON 将被缩小并转换为字符串，并返回结果字符数。仅适用于 `[BODY]` 占位符。|`len([BODY].username) > 8`|
|`has`|根据给定路径是否有效，返回 `true` 或 `false`。仅适用于 `[BODY]` 占位符。|`has([BODY].errors) == false`|
|`pat`|指定作为参数传递的字符串应被评估为模式。仅适用于 `==` 和 `!=`。|`[IP] == pat(192.168.*)`|
|`any`|指定作为参数传递的任何一个值都是有效值。仅适用于 `==` 和 `!=`。|`[BODY].ip == any(127.0.0.1, ::1)`|

> 💡 仅在需要时使用 `pat`。 `[STATUS] == pat(2*)`比`[STATUS] < 300`贵很多。

<a id="web"></a>
### 网络
允许您配置仪表板的服务方式和位置。

|范围|描述|默认|
|:---------------------------|:--------------------------------------------------------------------------------------------|:----------|
|`web`|网页配置|`{}`|
|`web.address`|收听地址。|`0.0.0.0`|
|`web.port`|要侦听的端口。|`8080`|
|`web.read-buffer-size`|从连接读取请求的缓冲区大小。还限制最大标头大小。|`8192`|
|`web.tls.certificate-file`|PEM 格式的 TLS 可选公共证书文件。|`""`|
|`web.tls.private-key-file`|PEM 格式的 TLS 可选私钥文件。|`""`|

<a id="ui"></a>
### 用户界面
允许您为仪表板的 UI 配置应用程序范围的默认值。用户可以使用浏览器的本地存储在本地覆盖其中一些参数。

|范围|描述|默认|
|:--------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------|
|`ui`|用户界面配置|`{}`|
|`ui.title`|[文档标题](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/title)。|`Health Dashboard ǀ Gatus`|
|`ui.description`|页面的元描述。|`Gatus is an advanced...`。|
|`ui.dashboard-heading`|标题和端点之间的仪表板标题|`Health Dashboard`|
|`ui.dashboard-subheading`|标头和端点之间的仪表板描述|`Monitor the health of your endpoints in real-time`|
|`ui.header`|仪表板顶部的标题。也用作 OIDC 登录页面上的标题。|`Gatus`|
|`ui.logo`|要显示的徽标的 URL。设置后，会显示在 OIDC 登录页面上的 Gatus 徽标旁边。|`""`|
|`ui.link`|单击徽标时打开链接。|`""`|
|`ui.favicon.default`|在 Web 浏览器选项卡或地址栏中显示的收藏夹默认图标。|`/favicon.ico`|
|`ui.favicon.size16x16`|在 Web 浏览器中显示的收藏夹图标，大小为 16x16。|`/favicon-16x16.png`|
|`ui.favicon.size32x32`|在 Web 浏览器中显示的收藏夹图标，大小为 32x32。|`/favicon-32x32.png`|
|`ui.buttons`|显示在标题下方的按钮列表。|`[]`|
|`ui.buttons[].name`|显示在按钮上的文本。|必需 `""`|
|`ui.buttons[].link`|单击按钮时打开链接。|必需 `""`|
|`ui.custom-css`|自定义CSS|`""`|
|`ui.dark-mode`|是否默认启用深色模式。请注意，这将被用户的操作系统主题首选项所取代。|`true`|
|`ui.default-sort-by`|仪表板中端点的默认排序选项。可以是 `name`、`group` 或 `health`。请注意，用户偏好会覆盖这一点。|`name`|
|`ui.default-filter-by`|仪表板中端点的默认过滤器选项。可以是 `none`、`failing` 或 `unstable`。请注意，用户偏好会覆盖这一点。|`none`|
|`ui.login-subtitle`|OIDC 登录页面上显示的副标题。|`System Monitoring Dashboard`|

<a id="announcements"></a>
### 公告
系统范围的公告允许您在状态页面顶部显示重要消息。这些可用于通知用户有关计划维护、持续存在的问题或一般信息。您可以使用 Markdown 来格式化您的公告。

这本质上就是某些状态页面所说的“事件通信”。

|范围|描述|默认|
|:----------------------------|:-------------------------------------------------------------------------------------------------------------------------|:---------|
|`announcements`|要显示的公告列表|`[]`|
|`announcements[].timestamp`|发布公告时的 UTC 时间戳（RFC3339 格式）|必需的|
|`announcements[].type`|公告类型。有效值：`outage`、`warning`、`information`、`operational`、`none`|`"none"`|
|`announcements[].message`|显示给用户的消息|必需的|
|`announcements[].archived`|是否归档公告。存档的公告显示在状态页面的底部而不是顶部。|`false`|

类型：
- **中断**：表示服务中断或严重问题（红色主题）
- **警告**：表示潜在问题或重要通知（黄色主题）
- **信息**：一般信息或更新（蓝色主题）
- **操作**：表示问题已解决或正常操作（绿色主题）
- **无**：没有特定严重性的中性公告（灰色主题，如果未指定则默认）

配置示例：
```yaml
announcements:
  - timestamp: 2025-11-07T14:00:00Z
    type: outage
    message: "Scheduled maintenance on database servers from 14:00 to 16:00 UTC"
  - timestamp: 2025-11-07T16:15:00Z
    type: operational
    message: "Database maintenance completed successfully. All systems operational."
  - timestamp: 2025-11-07T12:00:00Z
    type: information
    message: "New monitoring dashboard features will be deployed next week"
  - timestamp: 2025-11-06T09:00:00Z
    type: warning
    message: "Elevated API response times observed for US customers"
    archived: true
```

如果至少存档了一个公告，则状态页面底部将呈现 **过去的公告** 部分：
![Gatus 过去的公告部分](.github/assets/past-announcements.jpg)


<a id="storage"></a>
### 贮存
|范围|描述|默认|
|:------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------|:-----------|
|`storage`|存储配置|`{}`|
|`storage.path`|保存数据的路径。仅支持类型 `sqlite` 和 `postgres`。|`""`|
|`storage.type`|存储类型。有效类型：`memory`、`sqlite`、`postgres`。|`"memory"`|
|`storage.caching`|是否使用直写式缓存。缩短大型仪表板的加载时间。 <br />仅当 `storage.type` 为 `sqlite` 或 `postgres` 时受支持|`false`|
|`storage.maximum-number-of-results`|端点可以拥有的最大结果数|`100`|
|`storage.maximum-number-of-events`|端点可以拥有的最大事件数|`50`|

每个端点运行状况检查的结果以及正常运行时间和过去事件的数据必须保留
以便它们可以显示在仪表板上。这些参数允许您配置相关存储。

- 如果 `storage.type` 是 `memory`（默认）：
```yaml
# Note that this is the default value, and you can omit the storage configuration altogether to achieve the same result.
# Because the data is stored in memory, the data will not survive a restart.
storage:
  type: memory
  maximum-number-of-results: 200
  maximum-number-of-events: 5
```
- 如果 `storage.type` 为 `sqlite`，则 `storage.path` 不得为空：
```yaml
storage:
  type: sqlite
  path: data.db
```
有关示例，请参阅 [examples/docker-compose-sqlite-storage](.examples/docker-compose-sqlite-storage)。

- 如果 `storage.type` 是 `postgres`，则 `storage.path` 必须是连接 URL：
```yaml
storage:
  type: postgres
  path: "postgres://user:password@127.0.0.1:5432/gatus?sslmode=disable"
```
有关示例，请参阅 [examples/docker-compose-postgres-storage](.examples/docker-compose-postgres-storage)。


<a id="client-configuration"></a>
### 客户端配置
为了支持广泛的环境，每个受监控的端点都有一个独特的配置
客户端用于发送请求。

|范围|描述|默认|
|:---------------------------------------|:------------------------------------------------------------------------------|:----------------|
|`client.insecure`|是否跳过验证服务器的证书链和主机名。|`false`|
|`client.ignore-redirect`|是否忽略重定向（true）或遵循重定向（false，默认值）。|`false`|
|`client.timeout`|超时前的持续时间。|`10s`|
|`client.dns-resolver`|使用 `{proto}://{host}:{port}` 格式覆盖 DNS 解析器。|`""`|
|`client.oauth2`|OAuth2 客户端配置。|`{}`|
|`client.oauth2.token-url`|令牌端点 URL|需要 `""`|
|`client.oauth2.client-id`|应用于 `Client credentials flow` 的客户端 ID|需要 `""`|
|`client.oauth2.client-secret`|用于 `Client credentials flow` 的客户端密钥|需要 `""`|
|`client.oauth2.scopes[]`|应用于 `Client credentials flow` 的 `scopes` 列表。|需要 `[""]`|
|`client.proxy-url`|用于客户端的代理的 URL|`""`|
|`client.identity-aware-proxy`|Google Identity-Aware-Proxy 客户端配置。|`{}`|
|`client.identity-aware-proxy.audience`|身份感知代理受众。 （IAP oauth2 凭证的客户端 ID）|需要 `""`|
|`client.tls.certificate-file`|mTLS 配置的客户端证书（PEM 格式）的路径。|`""`|
|`client.tls.private-key-file`|mTLS 配置的客户端私钥（PEM 格式）的路径。|`""`|
|`client.tls.renegotiation`|提供的重新谈判支持类型。 （`never`、`freely`、`once`）。|`"never"`|
|`client.network`|用于 ICMP 端点客户端的网络（`ip`、`ip4` 或 `ip6`）。|`"ip"`|
|`client.tunnel`|用于此端点的 SSH 隧道的名称。请参阅[隧道](#tunneling)。|`""`|


> 📝 根据端点的类型，其中一些参数会被忽略。例如，不涉及证书
> 因此，在 ICMP 请求 (ping) 中，将该类型的端点的 `client.insecure` 设置为 `true` 不会执行任何操作。

这个默认配置如下：

```yaml
client:
  insecure: false
  ignore-redirect: false
  timeout: 10s
```

请注意，此配置仅在 `endpoints[]`、`alerting.mattermost` 和 `alerting.custom` 下可用。

以下是 `endpoints[]` 下的客户端配置示例：

```yaml
endpoints:
  - name: website
    url: "https://twin.sh/health"
    client:
      insecure: false
      ignore-redirect: false
      timeout: 10s
    conditions:
      - "[STATUS] == 200"
```

此示例显示如何指定自定义 DNS 解析器：

```yaml
endpoints:
  - name: with-custom-dns-resolver
    url: "https://your.health.api/health"
    client:
      dns-resolver: "tcp://8.8.8.8:53"
    conditions:
      - "[STATUS] == 200"
```

此示例显示如何使用 `client.oauth2` 配置来通过 `Bearer token` 查询后端 API：

```yaml
endpoints:
  - name: with-custom-oauth2
    url: "https://your.health.api/health"
    client:
      oauth2:
        token-url: https://your-token-server/token
        client-id: 00000000-0000-0000-0000-000000000000
        client-secret: your-client-secret
        scopes: ['https://your.health.api/.default']
    conditions:
      - "[STATUS] == 200"
```

此示例展示了如何使用 `client.identity-aware-proxy` 配置通过 Google Identity-Aware-Proxy 查询具有 `Bearer token` 的后端 API：

```yaml
endpoints:
  - name: with-custom-iap
    url: "https://my.iap.protected.app/health"
    client:
      identity-aware-proxy:
        audience: "XXXXXXXX-XXXXXXXXXXXX.apps.googleusercontent.com"
    conditions:
      - "[STATUS] == 200"
```

> 📝 请注意，Gatus 将在其环境中使用 [gcloud 默认凭据](https://cloud.google.com/docs/authentication/application-default-credentials) 来生成令牌。

此示例向您展示如何使用 `client.tls` 配置对后端 API 执行 mTLS 查询：

```yaml
endpoints:
  - name: website
    url: "https://your.mtls.protected.app/health"
    client:
      tls:
        certificate-file: /path/to/user_cert.pem
        private-key-file: /path/to/user_key.pem
        renegotiation: once
    conditions:
      - "[STATUS] == 200"
```

> 📝 请注意，如果在容器中运行，则必须将证书和密钥批量挂载到容器中。

<a id="tunneling"></a>
### 隧道技术
Gatus 支持 SSH 隧道，通过跳转主机或堡垒服务器监控内部服务。
这对于监控无法从部署 Gatus 的位置直接访问的服务特别有用。

SSH 隧道在 `tunneling` 部分中全局定义，然后在端点客户端配置中按名称引用。

|范围|描述|默认|
|:--------------------------------------|:------------------------------------------------------------|:--------------|
|`tunneling`|SSH 隧道配置|`{}`|
|`tunneling.<tunnel-name>`|命名 SSH 隧道的配置|`{}`|
|`tunneling.<tunnel-name>.type`|隧道类型（目前仅支持`SSH`）|必需 `""`|
|`tunneling.<tunnel-name>.host`|SSH 服务器主机名或 IP 地址|必需 `""`|
|`tunneling.<tunnel-name>.port`|SSH服务器端口|`22`|
|`tunneling.<tunnel-name>.username`|SSH 用户名|必需 `""`|
|`tunneling.<tunnel-name>.password`|SSH 密码（使用此密码或私钥）|`""`|
|`tunneling.<tunnel-name>.private-key`|PEM 格式的 SSH 私钥（使用此私钥或密码）|`""`|
|`client.tunnel`|用于此端点的隧道名称|`""`|

```yaml
tunneling:
  production:
    type: SSH
    host: "jumphost.example.com"
    username: "monitoring"
    private-key: |
      -----BEGIN RSA PRIVATE KEY-----
      MIIEpAIBAAKCAQEA...
      -----END RSA PRIVATE KEY-----

endpoints:
  - name: "internal-api"
    url: "http://internal-api.example.com:8080/health"
    client:
      tunnel: "production"
    conditions:
      - "[STATUS] == 200"
```

> ⚠️ **警告**:: 隧道可能会带来额外的延迟，特别是在频繁重试隧道连接的情况下。
> 这可能会导致响应时间测量不准确。


<a id="alerting"></a>
### 告警
Gatus 支持多个告警提供程序，例如 Slack 和 PagerDuty，并为每个提供程序支持不同的告警
具有可配置描述和阈值的各个端点。

告警在端点级别配置，如下所示：

|范围|描述|默认|
|:-------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------|
|`alerts`|给定端点的所有告警的列表。|`[]`|
|`alerts[].type`|告警类型。 <br />请参阅下表了解所有有效类型。|必需 `""`|
|`alerts[].enabled`|是否开启提醒。|`true`|
|`alerts[].failure-threshold`|触发告警之前所需的连续失败次数。|`3`|
|`alerts[].success-threshold`|将正在进行的事件标记为已解决之前连续成功的次数。|`2`|
|`alerts[].minimum-reminder-interval`|告警提醒之间的最小时间间隔。例如。 `"30m"`、`"1h45m30s"` 或 `"24h"`。如果为空或 `0`，则提醒被禁用。不能低于 `5m`。|`0`|
|`alerts[].send-on-resolved`|一旦触发的告警标记为已解决，是否发送通知。|`false`|
|`alerts[].description`|告警的描述。将包含在发送的告警中。|`""`|
|`alerts[].provider-override`|给定告警类型的告警提供程序配置覆盖|`{}`|

以下是端点级别的告警配置的示例：
```yaml
endpoints:
  - name: example
    url: "https://example.org"
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: slack
        description: "healthcheck failed"
        send-on-resolved: true
```

您还可以使用 `alerts[].provider-override` 覆盖全局提供程序配置，如下所示：
```yaml
endpoints:
  - name: example
    url: "https://example.org"
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: slack
        provider-override:
          webhook-url: "https://hooks.slack.com/services/**********/**********/**********"
```

> 📝 如果告警提供程序未正确配置，则使用提供程序类型配置的所有告警都将被
> 被忽略。

|范围|描述|默认|
|:---------------------------|:----------------------------------------------------------------------------------------------------------------------------------------|:--------|
|`alerting.awsses`|`awsses` 类型告警的配置。 <br />请参阅[配置 AWS SES 告警](#configuring-aws-ses-alerts)。|`{}`|
|`alerting.clickup`|`clickup` 类型告警的配置。 <br />请参阅[配置 ClickUp 告警](#configuring-clickup-alerts)。|`{}`|
|`alerting.custom`|针对故障或告警的自定义操作的配置。 <br />请参阅[配置自定义告警](#configuring-custom-alerts)。|`{}`|
|`alerting.datadog`|`datadog` 类型告警的配置。 <br />请参阅[配置数据狗告警](#configuring-datadog-alerts)。|`{}`|
|`alerting.discord`|`discord` 类型告警的配置。 <br />请参阅[配置 Discord 告警](#configuring-discord-alerts)。|`{}`|
|`alerting.email`|`email` 类型告警的配置。 <br />请参阅[配置电子邮件告警](#configuring-email-alerts)。|`{}`|
|`alerting.gitea`|`gitea` 类型告警的配置。 <br />请参阅[配置 Gitea 告警](#configuring-gitea-alerts)。|`{}`|
|`alerting.github`|`github` 类型告警的配置。 <br />请参阅[配置 GitHub 告警](#configuring-github-alerts)。|`{}`|
|`alerting.gitlab`|`gitlab` 类型告警的配置。 <br />请参阅[配置 GitLab 告警](#configuring-gitlab-alerts)。|`{}`|
|`alerting.googlechat`|`googlechat` 类型告警的配置。 <br />请参阅[配置 Google Chat 提醒](#configuring-google-chat-alerts)。|`{}`|
|`alerting.gotify`|`gotify` 类型告警的配置。 <br />请参阅[配置 Gotify 告警](#configuring-gotify-alerts)。|`{}`|
|`alerting.homeassistant`|`homeassistant` 类型告警的配置。 <br />请参阅[配置 HomeAssistant 告警](#configuring-homeassistant-alerts)。|`{}`|
|`alerting.ifttt`|`ifttt` 类型告警的配置。 <br />请参阅[配置 IFTTT 告警](#configuring-ifttt-alerts)。|`{}`|
|`alerting.ilert`|`ilert` 类型告警的配置。 <br />请参阅[配置警告告警](#configuring-ilert-alerts)。|`{}`|
|`alerting.incident-io`|`incident-io` 类型告警的配置。 <br />请参阅[配置 Incident.io 告警](#configuring-incidentio-alerts)。|`{}`|
|`alerting.line`|`line` 类型告警的配置。 <br />请参阅[配置Line 告警](#configuring-line-alerts)。|`{}`|
|`alerting.matrix`|`matrix` 类型告警的配置。 <br />请参阅[配置Matrix 告警](#configuring-matrix-alerts)。|`{}`|
|`alerting.mattermost`|`mattermost` 类型告警的配置。 <br />请参阅[配置 Mattermost 告警](#configuring-mattermost-alerts)。|`{}`|
|`alerting.messagebird`|`messagebird` 类型告警的配置。 <br />请参阅[配置 Messagebird 告警](#configuring-messagebird-alerts)。|`{}`|
|`alerting.n8n`|`n8n` 类型告警的配置。 <br />请参阅[配置 n8n 告警](#configuring-n8n-alerts)。|`{}`|
|`alerting.newrelic`|`newrelic` 类型告警的配置。 <br />请参阅[配置New Relic告警](#configuring-new-relic-alerts)。|`{}`|
|`alerting.ntfy`|`ntfy` 类型告警的配置。 <br />请参阅[配置 Ntfy 告警](#configuring-ntfy-alerts)。|`{}`|
|`alerting.opsgenie`|`opsgenie` 类型告警的配置。 <br />请参阅[配置 Opsgenie 告警](#configuring-opsgenie-alerts)。|`{}`|
|`alerting.pagerduty`|`pagerduty` 类型告警的配置。 <br />请参阅[配置 PagerDuty 告警](#configuring-pagerduty-alerts)。|`{}`|
|`alerting.plivo`|`plivo` 类型告警的配置。 <br />请参阅[配置 Plivo 告警](#configuring-plivo-alerts)。|`{}`|
|`alerting.pushover`|`pushover` 类型告警的配置。 <br />请参阅[配置 Pushover 告警](#configuring-pushover-alerts)。|`{}`|
|`alerting.rocketchat`|`rocketchat` 类型告警的配置。 <br />请参阅[配置 Rocket.Chat 告警](#configuring-rocketchat-alerts)。|`{}`|
|`alerting.sendgrid`|`sendgrid` 类型告警的配置。 <br />请参阅[配置 SendGrid 告警](#configuring-sendgrid-alerts)。|`{}`|
|`alerting.signal`|`signal` 类型告警的配置。 <br />请参阅[配置Signal 告警](#configuring-signal-alerts)。|`{}`|
|`alerting.signl4`|`signl4` 类型告警的配置。 <br />请参阅[配置 SIGNL4 告警](#configuring-signl4-alerts)。|`{}`|
|`alerting.slack`|`slack` 类型告警的配置。 <br />请参阅[配置 Slack 告警](#configuring-slack-alerts)。|`{}`|
|`alerting.splunk`|`splunk` 类型告警的配置。 <br />请参阅[配置 Splunk 告警](#configuring-splunk-alerts)。|`{}`|
|`alerting.squadcast`|`squadcast` 类型告警的配置。 <br />请参阅[配置 Squadcast 告警](#configuring-squadcast-alerts)。|`{}`|
|`alerting.teams`|`teams` 类型告警的配置。 *（已弃用）* <br />请参阅[配置团队告警](#configuring-teams-alerts-deprecated)。|`{}`|
|`alerting.teams-workflows`|`teams-workflows` 类型告警的配置。 <br />请参阅[配置 Teams 工作流告警](#configuring-teams-workflow-alerts)。|`{}`|
|`alerting.telegram`|`telegram` 类型告警的配置。 <br />请参阅[配置Telegram 告警](#configuring-telegram-alerts)。|`{}`|
|`alerting.twilio`|`twilio` 类型告警的设置。 <br />请参阅[配置 Twilio 告警](#configuring-twilio-alerts)。|`{}`|
|`alerting.vonage`|`vonage` 类型告警的配置。 <br />请参阅[配置 Vonage 告警](#configuring-vonage-alerts)。|`{}`|
|`alerting.webex`|`webex` 类型告警的配置。 <br />请参阅[配置 Webex 告警](#configuring-webex-alerts)。|`{}`|
|`alerting.zapier`|`zapier` 类型告警的配置。 <br />请参阅[配置 Zapier 告警](#configuring-zapier-alerts)。|`{}`|
|`alerting.zulip`|`zulip` 类型告警的配置。 <br />请参阅[配置 Zulip 告警](#configuring-zulip-alerts)。|`{}`|


<a id="configuring-aws-ses-alerts"></a>
#### 配置 AWS SES 告警
|范围|描述|默认|
|:-------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.aws-ses`|`aws-ses` 类型告警的设置|`{}`|
|`alerting.aws-ses.access-key-id`|AWS 访问密钥 ID|可选 `""`|
|`alerting.aws-ses.secret-access-key`|AWS 秘密访问密钥|可选 `""`|
|`alerting.aws-ses.region`|AWS 区域|必需 `""`|
|`alerting.aws-ses.from`|发送电子邮件的电子邮件地址（应在 SES 中注册）|必需 `""`|
|`alerting.aws-ses.to`|要通知的电子邮件地址的逗号分隔列表|必需 `""`|
|`alerting.aws-ses.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.aws-ses.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.aws-ses.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.aws-ses.overrides[].*`|参见`alerting.aws-ses.*`参数|`{}`|

```yaml
alerting:
  aws-ses:
    access-key-id: "..."
    secret-access-key: "..."
    region: "us-east-1"
    from: "status@example.com"
    to: "user@example.com"

endpoints:
  - name: website
    interval: 30s
    url: "https://twin.sh/health"
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: aws-ses
        failure-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"
```

如果未定义 `access-key-id` 和 `secret-access-key`，Gatus 将回退到 IAM 身份验证。

确保您有能力使用 `ses:SendEmail`。


<a id="configuring-clickup-alerts"></a>
#### 配置 ClickUp 告警

|范围|描述|默认|
| :--------------------------------- | :----------------------------------------------------------------------------------------- | :------------ |
|`alerting.clickup`|`clickup` 类型告警的配置|`{}`|
|`alerting.clickup.list-id`|将在其中创建任务的 ClickUp 列表 ID|必需 `""`|
|`alerting.clickup.token`|ClickUp API 令牌|必需 `""`|
|`alerting.clickup.api-url`|自定义 API 网址|`https://api.clickup.com/api/v2`|
|`alerting.clickup.assignees`|要分配任务的用户 ID 列表|`[]`|
|`alerting.clickup.status`|创建任务的初始状态|`""`|
|`alerting.clickup.priority`|优先级：`urgent`、`high`、`normal`、`low` 或 `none`|`normal`|
|`alerting.clickup.notify-all`|任务创建时是否通知所有受让人|`true`|
|`alerting.clickup.name`|自定义任务名称模板（支持占位符）|`Health Check: [ENDPOINT_GROUP]:[ENDPOINT_NAME]`|
|`alerting.clickup.content`|自定义任务内容模板（支持占位符）|`Triggered: [ENDPOINT_GROUP] - [ENDPOINT_NAME] - [ALERT_DESCRIPTION] - [RESULT_ERRORS]`|
|`alerting.clickup.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.clickup.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.clickup.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.clickup.overrides[].*`|参见`alerting.clickup.*`参数|`{}`|

当触发告警时，ClickUp 告警提供程序会在 ClickUp 列表中创建任务。如果端点告警上的 `send-on-resolved` 设置为 `true`，则告警解决后任务将自动关闭。

`name` 和 `content` 支持以下占位符：

- `[ENDPOINT_GROUP]` - 由 `endpoints[].group` 解析
- `[ENDPOINT_NAME]` - 由 `endpoints[].name` 解析
- `[ALERT_DESCRIPTION]` - 由 `endpoints[].alerts[].description` 解析
- `[RESULT_ERRORS]` - 解决健康评估错误

```yaml
alerting:
  clickup:
    list-id: "123456789"
    token: "pk_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    assignees:
      - "12345"
      - "67890"
    status: "in progress"
    priority: high
    name: "Health Check Alert: [ENDPOINT_GROUP] - [ENDPOINT_NAME]"
    content: "Alert triggered for [ENDPOINT_GROUP] - [ENDPOINT_NAME] - [ALERT_DESCRIPTION] - [RESULT_ERRORS]"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: clickup
        send-on-resolved: true
```

要获取 ClickUp API 令牌，请执行以下操作：[生成或重新生成个人 API 令牌](https://developer.clickup.com/docs/authentication#:~:text=the%20API%20docs.-,Generate%20or%20regenerate%20a%20Personal%20API%20Token,-Log%20in%20to)

要查找您的列表 ID：

1. 打开要在其中创建任务的 ClickUp 列表
2. 列表 ID 位于 URL 中：`https://app.clickup.com/{workspace_id}/v/l/li/{list_id}`

要查找受让人 ID：

1. 前往 `https://app.clickup.com/{workspace_id}/teams-pulse/teams/people`
2. 将鼠标悬停在团队成员上方
3. 单击 3 个点（溢出菜单）
3. 点击`Copy member ID`

<a id="configuring-datadog-alerts"></a>
#### 配置 Datadog 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:-------------------------------------|:-------------------------------------------------------------------------------------------|:------------------|
|`alerting.datadog`|`datadog` 类型告警的配置|`{}`|
|`alerting.datadog.api-key`|数据狗 API 密钥|必需 `""`|
|`alerting.datadog.site`|Datadog 网站（例如 datadoghq.com、datadoghq.eu）|`"datadoghq.com"`|
|`alerting.datadog.tags`|要包含的附加标签|`[]`|
|`alerting.datadog.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.datadog.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.datadog.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.datadog.overrides[].*`|参见`alerting.datadog.*`参数|`{}`|

```yaml
alerting:
  datadog:
    api-key: "YOUR_API_KEY"
    site: "datadoghq.com"  # or datadoghq.eu for EU region
    tags:
      - "environment:production"
      - "team:platform"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: datadog
        send-on-resolved: true
```


<a id="configuring-discord-alerts"></a>
#### 配置Discord 告警
|范围|描述|默认|
|:-------------------------------------|:-------------------------------------------------------------------------------------------|:------------------------------------|
|`alerting.discord`|`discord` 类型告警的配置|`{}`|
|`alerting.discord.webhook-url`|Discord Webhook URL|必需 `""`|
|`alerting.discord.title`|通知标题|`":helmet_with_white_cross: Gatus"`|
|`alerting.discord.message-content`|嵌入之前发送的消息内容（对于 ping 用户/角色有用，例如 `<@123>`）|`""`|
|`alerting.discord.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.discord.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.discord.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.discord.overrides[].*`|参见`alerting.discord.*`参数|`{}`|

```yaml
alerting:
  discord:
    webhook-url: "https://discord.com/api/webhooks/**********/**********"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: discord
        description: "healthcheck failed"
        send-on-resolved: true
```


<a id="configuring-email-alerts"></a>
#### 配置电子邮件告警
|范围|描述|默认|
|:-----------------------------------|:----------------------------------------------------------------------------------------------|:--------------|
|`alerting.email`|`email` 类型告警的配置|`{}`|
|`alerting.email.from`|用于发送告警的电子邮件|必需 `""`|
|`alerting.email.username`|用于发送告警的 SMTP 服务器的用户名。如果为空，则使用 `alerting.email.from`。|`""`|
|`alerting.email.password`|用于发送告警的 SMTP 服务器的密码。如果为空，则不执行任何身份验证。|`""`|
|`alerting.email.host`|邮件服务器的主机（例如 `smtp.gmail.com`）|必需 `""`|
|`alerting.email.port`|邮件服务器正在侦听的端口（例如 `587`）|必需 `0`|
|`alerting.email.to`|将告警发送至的电子邮件地址|必需 `""`|
|`alerting.email.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.email.client.insecure`|是否跳过TLS验证|`false`|
|`alerting.email.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.email.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.email.overrides[].*`|参见`alerting.email.*`参数|`{}`|

```yaml
alerting:
  email:
    from: "from@example.com"
    username: "from@example.com"
    password: "hunter2"
    host: "mail.example.com"
    port: 587
    to: "recipient1@example.com,recipient2@example.com"
    client:
      insecure: false
    # You can also add group-specific to keys, which will
    # override the to key above for the specified groups
    overrides:
      - group: "core"
        to: "recipient3@example.com,recipient4@example.com"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: email
        description: "healthcheck failed"
        send-on-resolved: true

  - name: back-end
    group: core
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[CERTIFICATE_EXPIRATION] > 48h"
    alerts:
      - type: email
        description: "healthcheck failed"
        send-on-resolved: true
```

> ⚠ 有些邮件服务器速度慢得令人痛苦。


<a id="configuring-gitea-alerts"></a>
#### 配置 Gitea 告警

|范围|描述|默认|
|:--------------------------------|:-----------------------------------------------------------------------------------------------------------|:--------------|
|`alerting.gitea`|`gitea` 类型告警的配置|`{}`|
|`alerting.gitea.repository-url`|Gitea 存储库 URL（例如 `https://gitea.com/TwiN/example`）|必需 `""`|
|`alerting.gitea.token`|用于身份验证的个人访问令牌。 <br />必须至少有问题上的 RW 和元数据上的 RO。|必需 `""`|
|`alerting.gitea.default-alert`|默认告警配置。 <br />请参阅[设置默认告警](#setting-a-default-alert)。|不适用|

Gitea 告警提供商创建一个以 `alert(gatus):` 为前缀、以端点的显示为后缀的问题
每个告警的名称。如果端点告警上的 `send-on-resolved` 设置为 `true`，则该问题将自动解决
告警解决后关闭。

```yaml
alerting:
  gitea:
    repository-url: "https://gitea.com/TwiN/test"
    token: "349d63f16......"

endpoints:
  - name: example
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 75"
    alerts:
      - type: gitea
        failure-threshold: 2
        success-threshold: 3
        send-on-resolved: true
        description: "Everything's burning AAAAAHHHHHHHHHHHHHHH"
```

![Gitea 告警](.github/assets/gitea-alerts.png)


<a id="configuring-github-alerts"></a>
#### 配置 GitHub 告警

|范围|描述|默认|
|:---------------------------------|:-----------------------------------------------------------------------------------------------------------|:--------------|
|`alerting.github`|`github` 类型告警的配置|`{}`|
|`alerting.github.repository-url`|GitHub 存储库 URL（例如 `https://github.com/TwiN/example`）|必需 `""`|
|`alerting.github.token`|用于身份验证的个人访问令牌。 <br />必须至少有问题上的 RW 和元数据上的 RO。|必需 `""`|
|`alerting.github.default-alert`|默认告警配置。 <br />请参阅[设置默认告警](#setting-a-default-alert)。|不适用|

GitHub 告警提供商创建一个以 `alert(gatus):` 为前缀、以端点的显示为后缀的问题
每个告警的名称。如果端点告警上的 `send-on-resolved` 设置为 `true`，则该问题将自动解决
告警解决后关闭。

```yaml
alerting:
  github:
    repository-url: "https://github.com/TwiN/test"
    token: "github_pat_12345..."

endpoints:
  - name: example
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 75"
    alerts:
      - type: github
        failure-threshold: 2
        success-threshold: 3
        send-on-resolved: true
        description: "Everything's burning AAAAAHHHHHHHHHHHHHHH"
```

![GitHub 告警](.github/assets/github-alerts.png)


<a id="configuring-gitlab-alerts"></a>
#### 配置 GitLab 告警
|范围|描述|默认|
|:------------------------------------|:--------------------------------------------------------------------------------------------------------------------|:--------------|
|`alerting.gitlab`|`gitlab` 类型告警的配置|`{}`|
|`alerting.gitlab.webhook-url`|GitLab 告警 Webhook URL（例如 `https://gitlab.com/yourusername/example/alerts/notify/gatus/xxxxxxxxxxxxxxxx.json`）|必需 `""`|
|`alerting.gitlab.authorization-key`|GitLab 告警授权密钥。|必需 `""`|
|`alerting.gitlab.severity`|覆盖默认严重性（严重），可以是 `critical, high, medium, low, info, unknown` 之一|`""`|
|`alerting.gitlab.monitoring-tool`|覆盖监控工具名称（gatus）|`"gatus"`|
|`alerting.gitlab.environment-name`|设置gitlab环境的名称。需要在仪表板上显示告警。|`""`|
|`alerting.gitlab.service`|覆盖端点显示名称|`""`|
|`alerting.gitlab.default-alert`|默认告警配置。 <br />请参阅[设置默认告警](#setting-a-default-alert)。|不适用|

GitLab 告警提供程序创建一个以 `alert(gatus):` 为前缀、以端点的显示为后缀的告警
每个告警的名称。如果端点告警上的 `send-on-resolved` 设置为 `true`，告警将自动
告警解决后关闭。看
https://docs.gitlab.com/ee/operations/incident_management/integrations.html#configuration 配置端点。

```yaml
alerting:
  gitlab:
    webhook-url: "https://gitlab.com/hlidotbe/example/alerts/notify/gatus/xxxxxxxxxxxxxxxx.json"
    authorization-key: "12345"

endpoints:
  - name: example
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 75"
    alerts:
      - type: gitlab
        failure-threshold: 2
        success-threshold: 3
        send-on-resolved: true
        description: "Everything's burning AAAAAHHHHHHHHHHHHHHH"
```

![GitLab 告警](.github/assets/gitlab-alerts.png)


<a id="configuring-google-chat-alerts"></a>
#### 配置 Google Chat提醒
|范围|描述|默认|
|:----------------------------------------|:--------------------------------------------------------------------------------------------|:--------------|
|`alerting.googlechat`|`googlechat` 类型告警的配置|`{}`|
|`alerting.googlechat.webhook-url`|Google Chat Webhook 网址|必需 `""`|
|`alerting.googlechat.client`|客户端配置。 <br />参见[客户端配置](#client-configuration)。|`{}`|
|`alerting.googlechat.default-alert`|默认告警配置。 <br />请参阅[设置默认告警](#setting-a-default-alert)。|不适用|
|`alerting.googlechat.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.googlechat.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.googlechat.overrides[].*`|参见`alerting.googlechat.*`参数|`{}`|

```yaml
alerting:
  googlechat:
    webhook-url: "https://chat.googleapis.com/v1/spaces/*******/messages?key=**********&token=********"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: googlechat
        description: "healthcheck failed"
        send-on-resolved: true
```


<a id="configuring-gotify-alerts"></a>
#### 配置 Gotify 告警
|范围|描述|默认|
|:----------------------------------------------|:--------------------------------------------------------------------------------------------|:----------------------|
|`alerting.gotify`|`gotify` 类型告警的配置|`{}`|
|`alerting.gotify.server-url`|获取服务器 URL|必需 `""`|
|`alerting.gotify.token`|用于身份验证的令牌。|必需 `""`|
|`alerting.gotify.priority`|根据 Gotify 标准的告警优先级。|`5`|
|`alerting.gotify.title`|通知标题|`"Gatus: <endpoint>"`|
|`alerting.gotify.default-alert`|默认告警配置。 <br />请参阅[设置默认告警](#setting-a-default-alert)。|不适用|

```yaml
alerting:
  gotify:
    server-url: "https://gotify.example"
    token: "**************"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: gotify
        description: "healthcheck failed"
        send-on-resolved: true
```

以下是通知的示例：

![Gotify 通知](.github/assets/gotify-alerts.png)


<a id="configuring-homeassistant-alerts"></a>
#### 配置 HomeAssistant 告警
|范围|描述|默认值|
|:-------------------------------------------|:---------------------------------------------------------------------------------------|:--------------|
|`alerting.homeassistant.url`|HomeAssistant 实例 URL|必需 `""`|
|`alerting.homeassistant.token`|来自 HomeAssistant 的长期访问令牌|必需 `""`|
|`alerting.homeassistant.default-alert`|用于具有适当类型告警的端点的默认告警配置|`{}`|
|`alerting.homeassistant.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.homeassistant.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.homeassistant.overrides[].*`|参见`alerting.homeassistant.*`参数|`{}`|

```yaml
alerting:
  homeassistant:
    url: "http://homeassistant:8123"  # URL of your HomeAssistant instance
    token: "YOUR_LONG_LIVED_ACCESS_TOKEN"  # Long-lived access token from HomeAssistant

endpoints:
  - name: my-service
    url: "https://my-service.com"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: homeassistant
        enabled: true
        send-on-resolved: true
        description: "My service health check"
        failure-threshold: 3
        success-threshold: 2
```

告警将作为事件发送到 HomeAssistant，事件类型为 `gatus_alert`。事件数据包括：
- `status`：“已触发”或“已解决”
- `endpoint`：受监控端点的名称
- `description`：告警描述（如果提供）
- `conditions`：条件列表及其结果
- `failure_count`：连续失败次数（触发时）
- `success_count`：连续成功的次数（解决后）

您可以在 HomeAssistant 自动化中使用这些事件来：
- 发送通知
- 控制装置
- 触发场​​景
- 记录到历史记录
- 还有更多

HomeAssistant 自动化示例：
```yaml
automation:
  - alias: "Gatus Alert Handler"
    trigger:
      platform: event
      event_type: gatus_alert
    action:
      - service: notify.notify
        data_template:
          title: "Gatus Alert: {{ trigger.event.data.event_data.endpoint }}"
          message: >
            Status: {{ trigger.event.data.event_data.status }}
            {% if trigger.event.data.event_data.description %}
            Description: {{ trigger.event.data.event_data.description }}
            {% endif %}
            {% for condition in trigger.event.data.event_data.conditions %}
            {{ '✅' if condition.success else '❌' }} {{ condition.condition }}
            {% endfor %}
```

要获取 HomeAssistant 长期访问令牌：
1. 打开家庭助理
2. 单击您的个人资料名称（左下角）
3. 向下滚动到“长期访问令牌”
4. 点击“创建令牌”
5. 为其命名（例如“Gatus”）
6. 复制令牌 - 您只会看到它一次！


<a id="configuring-ifttt-alerts"></a>
#### 配置 IFTTT 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:-----------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.ifttt`|`ifttt` 类型告警的配置|`{}`|
|`alerting.ifttt.webhook-key`|IFTTT Webhook 密钥|必需 `""`|
|`alerting.ifttt.event-name`|IFTTT 活动名称|必需 `""`|
|`alerting.ifttt.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.ifttt.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.ifttt.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.ifttt.overrides[].*`|参见`alerting.ifttt.*`参数|`{}`|

```yaml
alerting:
  ifttt:
    webhook-key: "YOUR_WEBHOOK_KEY"
    event-name: "gatus_alert"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: ifttt
        send-on-resolved: true
```


<a id="configuring-ilert-alerts"></a>
#### 配置 Ilert 告警
|范围|描述|默认|
|:-----------------------------------|:-------------------------------------------------------------------------------------------|:--------|
|`alerting.ilert`|`ilert` 类型告警的配置|`{}`|
|`alerting.ilert.integration-key`|ilert 告警源集成密钥|`""`|
|`alerting.ilert.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.ilert.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.ilert.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.ilert.overrides[].*`|参见`alerting.ilert.*`参数|`{}`|

强烈建议将 `endpoints[].alerts[].send-on-resolved` 设置为 `true` 以进行告警
类型为 `ilert`，因为与其他告警不同，设置产生的操作表示
`true` 的参数不会创建另一个告警，而是将告警标记为已解决
相反。

行为：
- 默认情况下，`alerting.ilert.integration-key` 用作集成密钥
- 如果正在评估的端点属于与 `alerting.ilert.overrides[].group` 的值匹配的组 (`endpoints[].group`)，则提供程序将使用该覆盖的集成密钥而不是 `alerting.ilert.integration-key` 的集成密钥

```yaml
alerting:
  ilert:
    integration-key: "********************************"
    # You can also add group-specific integration keys, which will
    # override the integration key above for the specified groups
    overrides:
      - group: "core"
        integration-key: "********************************"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: ilert
        failure-threshold: 3
        success-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-incidentio-alerts"></a>
#### 配置 Incident.io 告警
|范围|描述|默认|
|:-----------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.incident-io`|`incident-io` 类型告警的配置|`{}`|
|`alerting.incident-io.url`|触发告警事件的 url。|必需 `""`|
|`alerting.incident-io.auth-token`|用于身份验证的令牌。|必需 `""`|
|`alerting.incident-io.source-url`|来源网址|`""`|
|`alerting.incident-io.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.incident-io.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.incident-io.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.incident-io.overrides[].*`|参见`alerting.incident-io.*`参数|`{}`|

```yaml
alerting:
  incident-io:
    url: "*****************"
    auth-token: "********************************************"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: incident-io
        description: "healthcheck failed"
        send-on-resolved: true
```
为了获取所需的告警源配置 ID 和身份验证令牌，您必须配置 HTTP 告警源。

> **_注意：_** 源配置 ID 的格式为 `https://api.incident.io/v2/alert_events/http/$ID`，令牌预计将作为不记名令牌传递，如下所示：`Authorization: Bearer $TOKEN`


<a id="configuring-line-alerts"></a>
#### 配置Line 告警

|范围|描述|默认|
|:-------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.line`|`line` 类型告警的配置|`{}`|
|`alerting.line.channel-access-token`|Line Messaging API 通道访问令牌|必需 `""`|
|`alerting.line.user-ids`|要发送消息的线路用户 ID 列表（可以是用户 ID、房间 ID 或组 ID）|必需 `[]`|
|`alerting.line.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.line.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.line.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.line.overrides[].*`|参见`alerting.line.*`参数|`{}`|

```yaml
alerting:
  line:
    channel-access-token: "YOUR_CHANNEL_ACCESS_TOKEN"
    user-ids:
      - "U1234567890abcdef" # This can be a group id, room id or user id
      - "U2345678901bcdefg"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: line
        send-on-resolved: true
```


<a id="configuring-matrix-alerts"></a>
#### 配置Matrix 告警
|范围|描述|默认|
|:-----------------------------------------|:-------------------------------------------------------------------------------------------|:-----------------------------------|
|`alerting.matrix`|`matrix` 类型告警的配置|`{}`|
|`alerting.matrix.server-url`|家庭服务器网址|`https://matrix-client.matrix.org`|
|`alerting.matrix.access-token`|机器人用户访问令牌（请参阅 https://webapps.stackexchange.com/q/131056）|必需 `""`|
|`alerting.matrix.internal-room-id`|要将告警发送到的房间的内部房间 ID（可以在房间设置 > 高级中找到）|必需 `""`|
|`alerting.matrix.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.matrix.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.matrix.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.matrix.overrides[].*`|参见`alerting.matrix.*`参数|`{}`|

```yaml
alerting:
  matrix:
    server-url: "https://matrix-client.matrix.org"
    access-token: "123456"
    internal-room-id: "!example:matrix.org"

endpoints:
  - name: website
    interval: 5m
    url: "https://twin.sh/health"
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: matrix
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-mattermost-alerts"></a>
#### 配置 Mattermost 告警
|范围|描述|默认|
|:----------------------------------------------|:--------------------------------------------------------------------------------------------|:--------------|
|`alerting.mattermost`|`mattermost` 类型告警的配置|`{}`|
|`alerting.mattermost.webhook-url`|Mattermost Webhook URL|必需 `""`|
|`alerting.mattermost.channel`|Mattermost 频道名称覆盖（可选）|`""`|
|`alerting.mattermost.client`|客户端配置。 <br />参见[客户端配置](#client-configuration)。|`{}`|
|`alerting.mattermost.default-alert`|默认告警配置。 <br />请参阅[设置默认告警](#setting-a-default-alert)。|不适用|
|`alerting.mattermost.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.mattermost.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.mattermost.overrides[].*`|参见`alerting.mattermost.*`参数|`{}`|

```yaml
alerting:
  mattermost:
    webhook-url: "http://**********/hooks/**********"
    client:
      insecure: true

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: mattermost
        description: "healthcheck failed"
        send-on-resolved: true
```

以下是通知的示例：

![Mattermost 通知](.github/assets/mattermost-alerts.png)


<a id="configuring-messagebird-alerts"></a>
#### 配置 Messagebird 告警
|范围|描述|默认|
|:-------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.messagebird`|`messagebird` 类型告警的配置|`{}`|
|`alerting.messagebird.access-key`|Messagebird 访问密钥|必需 `""`|
|`alerting.messagebird.originator`|消息的发送者|必需 `""`|
|`alerting.messagebird.recipients`|消息的接收者|必需 `""`|
|`alerting.messagebird.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|

使用 Messagebird 发送 **SMS** 短信告警的示例：
```yaml
alerting:
  messagebird:
    access-key: "..."
    originator: "31619191918"
    recipients: "31619191919,31619191920"

endpoints:
  - name: website
    interval: 5m
    url: "https://twin.sh/health"
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: messagebird
        failure-threshold: 3
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-new-relic-alerts"></a>
#### 配置新遗迹告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:--------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.newrelic`|`newrelic` 类型告警的配置|`{}`|
|`alerting.newrelic.api-key`|新 Relic API 密钥|必需 `""`|
|`alerting.newrelic.account-id`|新遗物帐户 ID|必需 `""`|
|`alerting.newrelic.region`|地区（美国或欧盟）|`"US"`|
|`alerting.newrelic.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.newrelic.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.newrelic.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.newrelic.overrides[].*`|参见`alerting.newrelic.*`参数|`{}`|

```yaml
alerting:
  newrelic:
    api-key: "YOUR_API_KEY"
    account-id: "1234567"
    region: "US"  # or "EU" for European region

endpoints:
  - name: example
    url: "https://example.org"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: newrelic
        send-on-resolved: true
```


<a id="configuring-n8n-alerts"></a>
#### 配置 n8n 告警
|范围|描述|默认|
|:---------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.n8n`|`n8n` 类型告警的配置|`{}`|
|`alerting.n8n.webhook-url`|n8n webhook URL|必需 `""`|
|`alerting.n8n.title`|发送到 n8n 的告警标题|`""`|
|`alerting.n8n.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.n8n.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.n8n.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.n8n.overrides[].*`|参见`alerting.n8n.*`参数|`{}`|

[n8n](https://n8n.io/) 是一个工作流自动化平台，允许您使用 Webhooks 跨不同应用程序和服务自动执行任务。

请参阅 [n8n-nodes-gatus-trigger](https://github.com/TwiN/n8n-nodes-gatus-trigger) 了解可用作触发器的 n8n 社区节点。

例子：
```yaml
alerting:
  n8n:
    webhook-url: "https://your-n8n-instance.com/webhook/your-webhook-id"
    title: "Gatus Monitoring"
    default-alert:
      send-on-resolved: true

endpoints:
  - name: example
    url: "https://example.org"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: n8n
        description: "Health check alert"
```

发送到 n8n webhook 的 JSON 负载将包括：
- `title`：配置的标题
- `endpoint_name`：端点名称
- `endpoint_group`：端点组（如果有）
- `endpoint_url`：正在监控的 URL
- `alert_description`：自定义告警描述
- `resolved`：指示告警是否已解决的布尔值
- `message`：人类可读的告警消息
- `condition_results`：条件结果数组及其成功状态


<a id="configuring-ntfy-alerts"></a>
#### 配置 Ntfy 告警
|范围|描述|默认|
|:-------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------|:------------------|
|`alerting.ntfy`|`ntfy` 类型告警的配置|`{}`|
|`alerting.ntfy.topic`|将发送告警的主题|必需 `""`|
|`alerting.ntfy.url`|目标服务器的URL|`https://ntfy.sh`|
|`alerting.ntfy.token`|[访问令牌](https://docs.ntfy.sh/publish/#access-tokens) 用于受限主题|`""`|
|`alerting.ntfy.email`|用于其他电子邮件通知的电子邮件地址|`""`|
|`alerting.ntfy.click`|单击通知时打开网站|`""`|
|`alerting.ntfy.priority`|告警的优先级|`3`|
|`alerting.ntfy.disable-firebase`|是否应禁用通过 firebase 的消息推送传递。 [ntfy.sh默认启用](https://docs.ntfy.sh/publish/#disable-firebase)|`false`|
|`alerting.ntfy.disable-cache`|是否应禁用服务器端消息缓存。 [ntfy.sh默认启用](https://docs.ntfy.sh/publish/#message-caching)|`false`|
|`alerting.ntfy.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.ntfy.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.ntfy.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.ntfy.overrides[].*`|参见`alerting.ntfy.*`参数|`{}`|

[ntfy](https://github.com/binwiederhier/ntfy) 是一个很棒的项目，它允许您订阅桌面
和移动通知，使其成为 Gatus 的绝佳补充。

例子：
```yaml
alerting:
  ntfy:
    topic: "gatus-test-topic"
    priority: 2
    token: faketoken
    default-alert:
      failure-threshold: 3
      send-on-resolved: true
    # You can also add group-specific to keys, which will
    # override the to key above for the specified groups
    overrides:
      - group: "other"
        topic: "gatus-other-test-topic"
        priority: 4
        click: "https://example.com"

endpoints:
  - name: website
    interval: 5m
    url: "https://twin.sh/health"
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: ntfy
  - name: other example
    group: other
    interval: 30m
    url: "https://example.com"
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
    alerts:
      - type: ntfy
        description: example
```


<a id="configuring-opsgenie-alerts"></a>
#### 配置 Opsgenie 告警
|范围|描述|默认|
|:----------------------------------|:-------------------------------------------------------------------------------------------|:---------------------|
|`alerting.opsgenie`|`opsgenie` 类型告警的配置|`{}`|
|`alerting.opsgenie.api-key`|Opsgenie API 密钥|必需 `""`|
|`alerting.opsgenie.priority`|告警的优先级。|`P1`|
|`alerting.opsgenie.source`|告警的源字段。|`gatus`|
|`alerting.opsgenie.entity-prefix`|实体字段前缀。|`gatus-`|
|`alerting.opsgenie.alias-prefix`|别名字段前缀。|`gatus-healthcheck-`|
|`alerting.opsgenie.tags`|告警标签。|`[]`|
|`alerting.opsgenie.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|

Opsgenie 提供商将自动打开和关闭告警。

```yaml
alerting:
  opsgenie:
    api-key: "00000000-0000-0000-0000-000000000000"
```


<a id="configuring-pagerduty-alerts"></a>
#### 配置 PagerDuty 告警
|范围|描述|默认|
|:---------------------------------------|:-------------------------------------------------------------------------------------------|:--------|
|`alerting.pagerduty`|`pagerduty` 类型告警的配置|`{}`|
|`alerting.pagerduty.integration-key`|PagerDuty 事件 API v2 集成密钥|`""`|
|`alerting.pagerduty.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.pagerduty.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.pagerduty.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.pagerduty.overrides[].*`|参见`alerting.pagerduty.*`参数|`{}`|

强烈建议将 `endpoints[].alerts[].send-on-resolved` 设置为 `true` 以进行告警
类型为 `pagerduty`，因为与其他告警不同，设置产生的操作表示
`true` 的参数不会创建另一个事件，而是将事件标记为已解决
改为 PagerDuty。

行为：
- 默认情况下，`alerting.pagerduty.integration-key` 用作集成密钥
- 如果正在评估的端点属于与 `alerting.pagerduty.overrides[].group` 的值匹配的组 (`endpoints[].group`)，则提供程序将使用该覆盖的集成密钥而不是 `alerting.pagerduty.integration-key` 的集成密钥

```yaml
alerting:
  pagerduty:
    integration-key: "********************************"
    # You can also add group-specific integration keys, which will
    # override the integration key above for the specified groups
    overrides:
      - group: "core"
        integration-key: "********************************"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: pagerduty
        failure-threshold: 3
        success-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"

  - name: back-end
    group: core
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[CERTIFICATE_EXPIRATION] > 48h"
    alerts:
      - type: pagerduty
        failure-threshold: 3
        success-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-plivo-alerts"></a>
#### 配置 Plivo 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:-----------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.plivo`|`plivo` 类型告警的配置|`{}`|
|`alerting.plivo.auth-id`|Plivo 身份验证 ID|必需 `""`|
|`alerting.plivo.auth-token`|Plivo 身份验证令牌|必需 `""`|
|`alerting.plivo.from`|用于发送短信的电话号码|必需 `""`|
|`alerting.plivo.to`|要发送短信的电话号码列表|必需 `[]`|
|`alerting.plivo.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.plivo.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.plivo.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.plivo.overrides[].*`|参见`alerting.plivo.*`参数|`{}`|

```yaml
alerting:
  plivo:
    auth-id: "MAXXXXXXXXXXXXXXXXXX"
    auth-token: "your-auth-token"
    from: "+1234567890"
    to:
      - "+0987654321"
      - "+1122334455"

endpoints:
  - name: website
    interval: 30s
    url: "https://twin.sh/health"
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: plivo
        failure-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-pushover-alerts"></a>
#### 配置 Pushover 告警
|范围|描述|默认|
|:--------------------------------------|:-------------------------------------------------------------------------------------------------------------|:----------------------|
|`alerting.pushover`|`pushover` 类型告警的配置|`{}`|
|`alerting.pushover.application-token`|Pushover 应用令牌|`""`|
|`alerting.pushover.user-key`|用户或组密钥|`""`|
|`alerting.pushover.title`|通过 Pushover 发送的所有消息的固定标题|`"Gatus: <endpoint>"`|
|`alerting.pushover.priority`|所有消息的优先级，范围从 -2（非常低）到 2（紧急）|`0`|
|`alerting.pushover.resolved-priority`|覆盖已解决消息的优先级，范围从 -2（非常低）到 2（紧急）|`0`|
|`alerting.pushover.sound`|所有消息的声音<br />请参阅[声音](https://pushover.net/api#sounds)了解所有有效选项。|`""`|
|`alerting.pushover.ttl`|设置要从 Pushover 通知中自动删除的消息的生存时间|`0`|
|`alerting.pushover.device`|发送消息的设备（可选）<br/>有关详细信息，请参阅[设备](https://pushover.net/api#identifiers)|`""`（所有设备）|
|`alerting.pushover.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|

```yaml
alerting:
  pushover:
    application-token: "******************************"
    user-key: "******************************"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: pushover
        failure-threshold: 3
        success-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-rocketchat-alerts"></a>
#### 配置 Rocket.Chat 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:----------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.rocketchat`|`rocketchat` 类型告警的配置|`{}`|
|`alerting.rocketchat.webhook-url`|Rocket.Chat 传入 webhook URL|必需 `""`|
|`alerting.rocketchat.channel`|可选通道覆盖|`""`|
|`alerting.rocketchat.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.rocketchat.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.rocketchat.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.rocketchat.overrides[].*`|参见`alerting.rocketchat.*`参数|`{}`|

```yaml
alerting:
  rocketchat:
    webhook-url: "https://your-rocketchat.com/hooks/YOUR_WEBHOOK_ID/YOUR_TOKEN"
    channel: "#alerts"  # Optional

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: rocketchat
        send-on-resolved: true
```


<a id="configuring-sendgrid-alerts"></a>
#### 配置 SendGrid 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:--------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.sendgrid`|`sendgrid` 类型告警的配置|`{}`|
|`alerting.sendgrid.api-key`|SendGrid API 密钥|必需 `""`|
|`alerting.sendgrid.from`|发送电子邮件地址|必需 `""`|
|`alerting.sendgrid.to`|用于发送告警的电子邮件地址（对于多个收件人，以逗号分隔）|必需 `""`|
|`alerting.sendgrid.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.sendgrid.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.sendgrid.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.sendgrid.overrides[].*`|参见`alerting.sendgrid.*`参数|`{}`|

```yaml
alerting:
  sendgrid:
    api-key: "SG.xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    from: "alerts@example.com"
    to: "admin@example.com,ops@example.com"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: sendgrid
        send-on-resolved: true
```


<a id="configuring-signal-alerts"></a>
#### 配置Signal 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.signal`|`signal` 类型告警的配置|`{}`|
|`alerting.signal.api-url`|Signal API URL（例如 signal-cli-rest-api 实例）|必需 `""`|
|`alerting.signal.number`|发件人电话号码|必需 `""`|
|`alerting.signal.recipients`|收件人电话号码列表|必需 `[]`|
|`alerting.signal.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.signal.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.signal.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.signal.overrides[].*`|参见`alerting.signal.*`参数|`{}`|

```yaml
alerting:
  signal:
    api-url: "http://localhost:8080"
    number: "+1234567890"
    recipients:
      - "+0987654321"
      - "+1122334455"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: signal
        send-on-resolved: true
```


<a id="configuring-signl4-alerts"></a>
#### 配置 SIGNL4 告警

SIGNL4 是一种移动告警和事件管理服务，可通过移动推送、短信、语音通话和电子邮件向团队成员发送关键告警。

|范围|描述|默认|
|:------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.signl4`|`signl4` 类型告警的配置|`{}`|
|`alerting.signl4.team-secret`|SIGNL4 团队秘密（webhook URL 的一部分）|必需 `""`|
|`alerting.signl4.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.signl4.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.signl4.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.signl4.overrides[].*`|参见`alerting.signl4.*`参数|`{}`|

```yaml
alerting:
  signl4:
    team-secret: "your-team-secret-here"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: signl4
        send-on-resolved: true
```


<a id="configuring-slack-alerts"></a>
#### 配置 Slack 告警
|范围|描述|默认|
|:-----------------------------------|:-------------------------------------------------------------------------------------------|:------------------------------------|
|`alerting.slack`|`slack` 类型告警的配置|`{}`|
|`alerting.slack.webhook-url`|Slack Webhook URL|必需 `""`|
|`alerting.slack.title`|通知标题|`":helmet_with_white_cross: Gatus"`|
|`alerting.slack.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.slack.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.slack.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.slack.overrides[].*`|参见`alerting.slack.*`参数|`{}`|

```yaml
alerting:
  slack:
    webhook-url: "https://hooks.slack.com/services/**********/**********/**********"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: slack
        description: "healthcheck failed 3 times in a row"
        send-on-resolved: true
      - type: slack
        failure-threshold: 5
        description: "healthcheck failed 5 times in a row"
        send-on-resolved: true
```

以下是通知的示例：

![Slack 通知](.github/assets/slack-alerts.png)


<a id="configuring-splunk-alerts"></a>
#### 配置 Splunk 告警

|范围|描述|默认|
|:------------------------------------|:-------------------------------------------------------------------------------------------|:----------------|
|`alerting.splunk`|`splunk` 类型告警的配置|`{}`|
|`alerting.splunk.hec-url`|Splunk HEC（HTTP 事件收集器）URL|必需 `""`|
|`alerting.splunk.hec-token`|Splunk HEC 令牌|必需 `""`|
|`alerting.splunk.source`|事件源|`"gatus"`|
|`alerting.splunk.sourcetype`|事件源类型|`"gatus:alert"`|
|`alerting.splunk.index`|斯普伦克指数|`""`|
|`alerting.splunk.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.splunk.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.splunk.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.splunk.overrides[].*`|参见`alerting.splunk.*`参数|`{}`|

```yaml
alerting:
  splunk:
    hec-url: "https://splunk.example.com:8088"
    hec-token: "YOUR_HEC_TOKEN"
    index: "main"  # Optional

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: splunk
        send-on-resolved: true
```


<a id="configuring-squadcast-alerts"></a>
#### 配置 Squacast 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:---------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.squadcast`|`squadcast` 类型告警的配置|`{}`|
|`alerting.squadcast.webhook-url`|Squacast Webhook URL|必需 `""`|
|`alerting.squadcast.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.squadcast.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.squadcast.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.squadcast.overrides[].*`|参见`alerting.squadcast.*`参数|`{}`|

```yaml
alerting:
  squadcast:
    webhook-url: "https://api.squadcast.com/v3/incidents/api/YOUR_API_KEY"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: squadcast
        send-on-resolved: true
```


<a id="configuring-teams-alerts-deprecated"></a>
#### 配置 Teams 告警 *（已弃用）*

> [！警告]
> **已弃用：** Microsoft Teams 中的 Office 365 连接器即将停用（[来源：Microsoft DevBlog](https://devblogs.microsoft.com/microsoft365dev/retirement-of-office-365-connectors-within-microsoft-teams/)）。
> 现有连接器将继续工作到 2025 年 12 月。新的 [Teams 工作流告警](#configuring-teams-workflow-alerts) 应与 Microsoft Workflows 一起使用，而不是此旧配置。

|范围|描述|默认|
|:-----------------------------------|:-------------------------------------------------------------------------------------------|:--------------------|
|`alerting.teams`|`teams` 类型告警的配置|`{}`|
|`alerting.teams.webhook-url`|团队 Webhook URL|必需 `""`|
|`alerting.teams.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.teams.title`|通知标题|`"&#x1F6A8; Gatus"`|
|`alerting.teams.client.insecure`|是否跳过TLS验证|`false`|
|`alerting.teams.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.teams.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.teams.overrides[].*`|参见`alerting.teams.*`参数|`{}`|

```yaml
alerting:
  teams:
    webhook-url: "https://********.webhook.office.com/webhookb2/************"
    client:
      insecure: false
    # You can also add group-specific to keys, which will
    # override the to key above for the specified groups
    overrides:
      - group: "core"
        webhook-url: "https://********.webhook.office.com/webhookb3/************"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: teams
        description: "healthcheck failed"
        send-on-resolved: true

  - name: back-end
    group: core
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[CERTIFICATE_EXPIRATION] > 48h"
    alerts:
      - type: teams
        description: "healthcheck failed"
        send-on-resolved: true
```

以下是通知的示例：

![团队通知](.github/assets/teams-alerts.png)


<a id="configuring-teams-workflow-alerts"></a>
#### 配置 Teams 工作流告警

> [！笔记]
> 此告警与 Microsoft Teams 的工作流程兼容。要设置工作流程并获取 Webhook URL，请遵循 [Microsoft 文档](https://support.microsoft.com/en-us/office/create-incoming-webhooks-with-workflows-for-microsoft-teams-8ae491c7-0394-4861-ba59-055e33f75498)。

|范围|描述|默认|
|:---------------------------------------------|:-------------------------------------------------------------------------------------------|:-------------------|
|`alerting.teams-workflows`|`teams` 类型告警的配置|`{}`|
|`alerting.teams-workflows.webhook-url`|团队 Webhook URL|必需 `""`|
|`alerting.teams-workflows.title`|通知标题|`"&#x26D1; Gatus"`|
|`alerting.teams-workflows.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.teams-workflows.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.teams-workflows.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.teams-workflows.overrides[].*`|参见`alerting.teams-workflows.*`参数|`{}`|

```yaml
alerting:
  teams-workflows:
    webhook-url: "https://********.webhook.office.com/webhookb2/************"
    # You can also add group-specific to keys, which will
    # override the to key above for the specified groups
    overrides:
      - group: "core"
        webhook-url: "https://********.webhook.office.com/webhookb3/************"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: teams-workflows
        description: "healthcheck failed"
        send-on-resolved: true

  - name: back-end
    group: core
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[CERTIFICATE_EXPIRATION] > 48h"
    alerts:
      - type: teams-workflows
        description: "healthcheck failed"
        send-on-resolved: true
```

以下是通知的示例：

![Teams 工作流程通知](.github/assets/teams-workflows-alerts.png)


<a id="configuring-telegram-alerts"></a>
#### 配置 Telegram 告警
|范围|描述|默认|
|:--------------------------------------|:-------------------------------------------------------------------------------------------|:---------------------------|
|`alerting.telegram`|`telegram` 类型告警的配置|`{}`|
|`alerting.telegram.token`|Telegram 机器人令牌|必需 `""`|
|`alerting.telegram.id`|电报聊天 ID|必需 `""`|
|`alerting.telegram.topic-id`|群组中的 Telegram 主题 ID 对应于 Telegram API 中的 `message_thread_id`|`""`|
|`alerting.telegram.api-url`|电报 API 网址|`https://api.telegram.org`|
|`alerting.telegram.client`|客户端配置。 <br />参见[客户端配置](#client-configuration)。|`{}`|
|`alerting.telegram.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.telegram.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.telegram.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.telegram.overrides[].*`|参见`alerting.telegram.*`参数|`{}`|

```yaml
alerting:
  telegram:
    token: "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11"
    id: "0123456789"
    topic-id: "7"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
    alerts:
      - type: telegram
        send-on-resolved: true
```

以下是通知的示例：

![电报通知](.github/assets/telegram-alerts.png)


<a id="configuring-twilio-alerts"></a>
#### 配置 Twilio 告警
|范围|描述|默认|
|:--------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.twilio`|`twilio` 类型告警的设置|`{}`|
|`alerting.twilio.sid`|Twilio 帐户 SID|必需 `""`|
|`alerting.twilio.token`|Twilio 身份验证令牌|必需 `""`|
|`alerting.twilio.from`|发送 Twilio 告警的号码|必需 `""`|
|`alerting.twilio.to`|发送 twilio 告警的号码|必需 `""`|
|`alerting.twilio.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|

通过以下附加参数支持自定义消息模板：

|范围|描述|默认|
|:----------------------------------------|:-------------------------------------------------------------------------------------------|:--------|
|`alerting.twilio.text-twilio-triggered`|用于触发告警的自定义消息模板。支持`[ENDPOINT]`、`[ALERT_DESCRIPTION]`|`""`|
|`alerting.twilio.text-twilio-resolved`|用于解决告警的自定义消息模板。支持`[ENDPOINT]`、`[ALERT_DESCRIPTION]`|`""`|

```yaml
alerting:
  twilio:
    sid: "..."
    token: "..."
    from: "+1-234-567-8901"
    to: "+1-234-567-8901"
    # Custom message templates using placeholders (optional)
    # Supports both old format {endpoint}/{description} and new format [ENDPOINT]/[ALERT_DESCRIPTION]
    text-twilio-triggered: "🚨 ALERT: [ENDPOINT] is down! [ALERT_DESCRIPTION]"
    text-twilio-resolved: "✅ RESOLVED: [ENDPOINT] is back up! [ALERT_DESCRIPTION]"

endpoints:
  - name: website
    interval: 30s
    url: "https://twin.sh/health"
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: twilio
        failure-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-vonage-alerts"></a>
#### 配置 Vonage 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.vonage`|`vonage` 类型告警的配置|`{}`|
|`alerting.vonage.api-key`|Vonage API 密钥|必需 `""`|
|`alerting.vonage.api-secret`|Vonage API 秘密|必需 `""`|
|`alerting.vonage.from`|发件人姓名或电话号码|必需 `""`|
|`alerting.vonage.to`|收件人电话号码|必需 `""`|
|`alerting.vonage.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.vonage.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.vonage.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.vonage.overrides[].*`|参见`alerting.vonage.*`参数|`{}`|

```yaml
alerting:
  vonage:
    api-key: "YOUR_API_KEY"
    api-secret: "YOUR_API_SECRET"
    from: "Gatus"
    to: "+1234567890"
```

向 Vonage 发送告警的示例：
```yaml
endpoints:
  - name: website
    url: "https://example.org"
    alerts:
      - type: vonage
        failure-threshold: 5
        send-on-resolved: true
        description: "healthcheck failed"
```


<a id="configuring-webex-alerts"></a>
#### 配置 Webex 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:-----------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.webex`|`webex` 类型告警的配置|`{}`|
|`alerting.webex.webhook-url`|Webex Teams webhook URL|必需 `""`|
|`alerting.webex.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.webex.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.webex.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.webex.overrides[].*`|参见`alerting.webex.*`参数|`{}`|

```yaml
alerting:
  webex:
    webhook-url: "https://webexapis.com/v1/webhooks/incoming/YOUR_WEBHOOK_ID"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: webex
        send-on-resolved: true
```


<a id="configuring-zapier-alerts"></a>
#### 配置 Zapier 告警

> ⚠️ **警告**：此告警提供程序尚未经过测试。如果您已经对其进行了测试并确认其有效，请删除此警告并创建拉取请求，或在 [#1223](https://github.com/TwiN/gatus/discussions/1223) 上评论提供程序是否按预期工作。感谢您的合作。

|范围|描述|默认|
|:--------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.zapier`|`zapier` 类型告警的配置|`{}`|
|`alerting.zapier.webhook-url`|Zapier Webhook URL|必需 `""`|
|`alerting.zapier.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.zapier.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.zapier.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.zapier.overrides[].*`|参见`alerting.zapier.*`参数|`{}`|

```yaml
alerting:
  zapier:
    webhook-url: "https://hooks.zapier.com/hooks/catch/YOUR_WEBHOOK_ID/"

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: zapier
        send-on-resolved: true
```


<a id="configuring-zulip-alerts"></a>
#### 配置 Zulip 告警
|范围|描述|默认|
|:-----------------------------------|:------------------------------------------------------------------------------------|:--------------|
|`alerting.zulip`|`zulip` 类型告警的配置|`{}`|
|`alerting.zulip.bot-email`|机器人电子邮件|必需 `""`|
|`alerting.zulip.bot-api-key`|机器人 API 密钥|必需 `""`|
|`alerting.zulip.domain`|完整的组织域（例如：yourZulipDomain.zulipchat.com）|必需 `""`|
|`alerting.zulip.channel-id`|Gatus 将向其发送告警的通道 ID|必需 `""`|
|`alerting.zulip.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.zulip.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.zulip.overrides[].*`|参见`alerting.zulip.*`参数|`{}`|

```yaml
alerting:
  zulip:
    bot-email: gatus-bot@some.zulip.org
    bot-api-key: "********************************"
    domain: some.zulip.org
    channel-id: 123456

endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: zulip
        description: "healthcheck failed"
        send-on-resolved: true
```


<a id="configuring-custom-alerts"></a>
#### 配置自定义告警
|范围|描述|默认|
|:------------------------------------|:-------------------------------------------------------------------------------------------|:--------------|
|`alerting.custom`|配置针对故障或告警的自定义操作|`{}`|
|`alerting.custom.url`|自定义告警请求​​ URL|必需 `""`|
|`alerting.custom.method`|请求方式|`GET`|
|`alerting.custom.body`|自定义告警请求​​正文。|`""`|
|`alerting.custom.headers`|自定义告警请求​​标头|`{}`|
|`alerting.custom.client`|客户端配置。 <br />参见[客户端配置](#client-configuration)。|`{}`|
|`alerting.custom.default-alert`|默认告警配置。 <br />参见[设置默认告警](#setting-a-default-alert)|不适用|
|`alerting.custom.overrides`|可能优先于默认配置的覆盖列表|`[]`|
|`alerting.custom.overrides[].group`|此配置将覆盖其配置的端点组|`""`|
|`alerting.custom.overrides[].*`|参见`alerting.custom.*`参数|`{}`|

虽然它们被称为告警，但您可以使用此功能来调用任何内容。

例如，您可以通过使用跟踪新部署的应用程序来自动回滚，并通过
利用 Gatus，您可以让 Gatus 在端点开始出现故障时调用该应用程序端点。您的申请
然后将检查开始失败的端点是否是最近部署的应用程序的一部分，如果是，
然后自动回滚。

此外，您可以在正文 (`alerting.custom.body`) 和 url (`alerting.custom.url`) 中使用以下占位符：
- `[ALERT_DESCRIPTION]`（从 `endpoints[].alerts[].description` 解析）
- `[ENDPOINT_NAME]`（从 `endpoints[].name` 解析）
- `[ENDPOINT_GROUP]`（从 `endpoints[].group` 解析）
- `[ENDPOINT_URL]`（从 `endpoints[].url` 解析）
- `[RESULT_ERRORS]`（从给定健康检查的健康评估中解析）
- `[RESULT_CONDITIONS]`（给定健康检查的健康评估的状况结果）
-
如果您有使用 `custom` 提供程序且 `send-on-resolved` 设置为 `true` 的告警，您可以使用
`[ALERT_TRIGGERED_OR_RESOLVED]` 占位符用于区分通知。
上述占位符将相应地替换为 `TRIGGERED` 或 `RESOLVED`，但可以修改
（详细信息见本节末尾）。

出于所有意图和目的，我们将使用 Slack Webhook 配置自定义告警，但您可以调用任何您想要的内容。
```yaml
alerting:
  custom:
    url: "https://hooks.slack.com/services/**********/**********/**********"
    method: "POST"
    body: |
      {
        "text": "[ALERT_TRIGGERED_OR_RESOLVED]: [ENDPOINT_GROUP] - [ENDPOINT_NAME] - [ALERT_DESCRIPTION] - [RESULT_ERRORS]"
      }
endpoints:
  - name: website
    url: "https://twin.sh/health"
    interval: 30s
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 300"
    alerts:
      - type: custom
        failure-threshold: 10
        success-threshold: 3
        send-on-resolved: true
        description: "health check failed"
```

请注意，您可以自定义 `[ALERT_TRIGGERED_OR_RESOLVED]` 占位符的解析值，如下所示：
```yaml
alerting:
  custom:
    placeholders:
      ALERT_TRIGGERED_OR_RESOLVED:
        TRIGGERED: "partial_outage"
        RESOLVED: "operational"
```
因此，本节第一个示例正文中的 `[ALERT_TRIGGERED_OR_RESOLVED]` 将替换为
触发告警时为 `partial_outage`，告警解决时为 `operational`。


<a id="setting-a-default-alert"></a>
#### 设置默认告警
|范围|描述|默认|
|:---------------------------------------------|:------------------------------------------------------------------------------|:--------|
|`alerting.*.default-alert.enabled`|是否开启提醒|不适用|
|`alerting.*.default-alert.failure-threshold`|触发告警之前所需的连续失败次数|不适用|
|`alerting.*.default-alert.success-threshold`|将正在进行的事件标记为已解决之前连续成功的次数|不适用|
|`alerting.*.default-alert.send-on-resolved`|一旦触发的告警标记为已解决，是否发送通知|不适用|
|`alerting.*.default-alert.description`|告警的描述。将包含在发送的告警中|不适用|

> ⚠ 即使您设置了提供商的默认告警，您仍必须在端点配置中指定告警的 `type`。

虽然您可以直接在端点定义中指定告警配置，但这很乏味，并且可能会导致非常糟糕的结果。
很长的配置文件。

为了避免此类问题，您可以使用每个提供程序配置中存在的 `default-alert` 参数：
```yaml
alerting:
  slack:
    webhook-url: "https://hooks.slack.com/services/**********/**********/**********"
    default-alert:
      description: "health check failed"
      send-on-resolved: true
      failure-threshold: 5
      success-threshold: 5
```

因此，您的 Gatus 配置看起来更加整洁：
```yaml
endpoints:
  - name: example
    url: "https://example.org"
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: slack

  - name: other-example
    url: "https://example.com"
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: slack
```

它还允许您执行以下操作：
```yaml
endpoints:
  - name: example
    url: "https://example.org"
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: slack
        failure-threshold: 5
      - type: slack
        failure-threshold: 10
      - type: slack
        failure-threshold: 15
```

当然，您也可以混合告警类型：
```yaml
alerting:
  slack:
    webhook-url: "https://hooks.slack.com/services/**********/**********/**********"
    default-alert:
      failure-threshold: 3
  pagerduty:
    integration-key: "********************************"
    default-alert:
      failure-threshold: 5

endpoints:
  - name: endpoint-1
    url: "https://example.org"
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: slack
      - type: pagerduty

  - name: endpoint-2
    url: "https://example.org"
    conditions:
      - "[STATUS] == 200"
    alerts:
      - type: slack
      - type: pagerduty
```


<a id="maintenance"></a>
### 维护
如果您有维护窗口，您可能不希望被告警打扰。
为此，您必须使用维护配置：

|范围|描述|默认|
|:-----------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------|
|`maintenance.enabled`|是否启用维护期|`true`|
|`maintenance.start`|维护时段开始的时间，格式为 `hh:mm`（例如 `23:00`）|必需 `""`|
|`maintenance.duration`|维护时段的持续时间（例如 `1h`、`30m`）|必需 `""`|
|`maintenance.timezone`|维护窗口格式的时区（例如 `Europe/Amsterdam`）。<br />请参阅 [tz 数据库时区列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 了解更多信息|`UTC`|
|`maintenance.every`|维护期适用的天数（例如 `[Monday, Thursday]`）。<br />如果留空，则维护时段每天适用|`[]`|

这是一个例子：
```yaml
maintenance:
  start: 23:00
  duration: 1h
  timezone: "Europe/Amsterdam"
  every: [Monday, Thursday]
```
请注意，您还可以在单​​独的行中指定每一天：
```yaml
maintenance:
  start: 23:00
  duration: 1h
  timezone: "Europe/Amsterdam"
  every:
    - Monday
    - Thursday
```
您还可以为每个端点指定维护时段：
```yaml
endpoints:
  - name: endpoint-1
    url: "https://example.org"
    maintenance-windows:
      - start: "07:30"
        duration: 40m
        timezone: "Europe/Berlin"
      - start: "14:30"
        duration: 1h
        timezone: "Europe/Berlin"
```


<a id="security"></a>
### 安全
|范围|描述|默认|
|:-----------------|:-----------------------------|:--------|
|`security`|安全配置|`{}`|
|`security.basic`|HTTP基本配置|`{}`|
|`security.oidc`|OpenID 连接配置|`{}`|


<a id="basic-authentication"></a>
#### 基本认证
|范围|描述|默认|
|:----------------------------------------|:-----------------------------------------------------------------------------------|:--------------|
|`security.basic`|HTTP基本配置|`{}`|
|`security.basic.username`|基本身份验证的用户名。|必需 `""`|
|`security.basic.password-bcrypt-base64`|密码使用 Bcrypt 进行哈希处理，然后使用 base64 进行编码以进行基本身份验证。|必需 `""`|

下面的示例将要求您使用用户名 `john.doe` 和密码 `hunter2` 进行身份验证：
```yaml
security:
  basic:
    username: "john.doe"
    password-bcrypt-base64: "JDJhJDEwJHRiMnRFakxWazZLdXBzRERQazB1TE8vckRLY05Yb1hSdnoxWU0yQ1FaYXZRSW1McmladDYu"
```

> ⚠ 确保仔细选择 bcrypt 哈希的成本。成本越高，计算哈希所需的时间就越长，
> 基本身份验证根据每个请求的哈希值验证密码。截至 2023 年 1 月 6 日，我建议成本为 9。


<a id="oidc"></a>
#### 开放式数据中心
|范围|描述|默认|
|:---------------------------------|:---------------------------------------------------------------|:--------------|
|`security.oidc`|OpenID 连接配置|`{}`|
|`security.oidc.issuer-url`|发行人网址|必需 `""`|
|`security.oidc.redirect-url`|重定向网址。必须以 `/authorization-code/callback` 结尾|必需 `""`|
|`security.oidc.client-id`|客户编号|必需 `""`|
|`security.oidc.client-secret`|客户秘密|必需 `""`|
|`security.oidc.scopes`|要求的范围。您唯一需要的示波器是 `openid`。|必需 `[]`|
|`security.oidc.allowed-subjects`|允许的科目列表。如果为空，则允许所有科目。|`[]`|
|`security.oidc.session-ttl`|会话生存时间（例如 `8h`、`1h30m`、`2h`）。|`8h`|

```yaml
security:
  oidc:
    issuer-url: "https://example.okta.com"
    redirect-url: "https://status.example.com/authorization-code/callback"
    client-id: "123456789"
    client-secret: "abcdefghijk"
    scopes: ["openid"]
    # You may optionally specify a list of allowed subjects. If this is not specified, all subjects will be allowed.
    #allowed-subjects: ["johndoe@example.com"]
    # You may optionally specify a session time-to-live. If this is not specified, defaults to 8 hours.
    #session-ttl: 8h
```

使困惑？阅读[使用 Auth0 通过 OIDC 保护 Gatus](https://twin.sh/articles/56/securing-gatus-with-oidc-using-auth0)。


<a id="tls-encryption"></a>
### 传输层安全性 (TLS) 加密
Gatus 支持使用 TLS 进行基本加密。为此，必须提供 PEM 格式的证书文件。

下面的示例显示了一个示例配置，该配置使 gatus 在端口 4443 上响应 HTTPS 请求：
```yaml
web:
  port: 4443
  tls:
    certificate-file: "certificate.crt"
    private-key-file: "private.key"
```


<a id="metrics"></a>
### 指标
要启用指标，必须将 `metrics` 设置为 `true`。这样做将在 `/metrics` 上公开 Prometheus 友好的指标
端点位于您的应用程序配置运行的同一端口 (`web.port`)。

|指标名称|类型|描述|标签|相关端点类型|
|:---------------------------------------------|:--------|:---------------------------------------------------------------------------|:--------------------------------|:------------------------|
|gatus_结果_总计|柜台|每个成功状态每个端点的结果数|键、组、名称、类型、成功|全部|
|gatus_结果_代码_总计|柜台|按代码显示的结果总数|键、组、名称、类型、代码|域名系统、HTTP|
|gatus_results_connected_total|柜台|成功建立连接的结果总数|键、组、名称、类型|全部|
|gatus_results_duration_秒|测量|请求的持续时间（以秒为单位）|键、组、名称、类型|全部|
|gatus_results_certificate_expiration_秒|测量|距离证书过期还有多少秒|键、组、名称、类型|HTTP、STARTTLS|
|gatus_results_domain_expiration_秒|测量|域过期之前的秒数|键、组、名称、类型|HTTP、STARTTLS|
|gatus_results_endpoint_success|测量|显示端点是否成功（0 失败，1 成功）|键、组、名称、类型|全部|

有关更多文档和示例，请参阅 [examples/docker-compose-grafana-prometheus](.examples/docker-compose-grafana-prometheus)。

<a id="custom-labels"></a>
#### 定制标签

您可以通过在 `extra-labels` 字段下定义键值对来向端点的 Prometheus 指标添加自定义标签。例如：

```yaml
endpoints:
  - name: front-end
    group: core
    url: "https://twin.sh/health"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
      - "[BODY].status == UP"
      - "[RESPONSE_TIME] < 150"
    extra-labels:
      environment: staging
```

<a id="connectivity"></a>
### 连接性
|范围|描述|默认|
|:--------------------------------|:-------------------------------------------|:--------------|
|`connectivity`|连接配置|`{}`|
|`connectivity.checker`|连接检查器配置|必需 `{}`|
|`connectivity.checker.target`|用于验证连接的主机|必需 `""`|
|`connectivity.checker.interval`|验证连接的时间间隔|`1m`|

虽然 Gatus 用于监控其他服务，但 Gatus 本身可能会失去与互联网的连接。
为了防止当 Gatus 本身不健康时 Gatus 报告端点不健康，您可以配置
Gatus 定期检查互联网连接。

当连接检查器认为连接已关闭时，所有端点执行都会被跳过。

```yaml
connectivity:
  checker:
    target: 1.1.1.1:53
    interval: 60s
```


<a id="remote-instances-experimental"></a>
### 远程实例（实验）
此功能允许您从远程 Gatus 实例检索端点状态。

有两个主要用例：
- 您有多个 Gatus 实例在不同的计算机上运行，​​并且您希望通过单个仪表板直观地公开状态
- 您有一个或多个不可公开访问的 Gatus 实例（例如在防火墙后面），并且您希望检索

这是一个实验性功能。它可能随时被删除或以破坏性的方式更新。此外，
此功能存在已知问题。如果您想提供一些反馈，请在 [#64](https://github.com/TwiN/gatus/issues/64) 中发表评论。
使用风险自负。

|范围|描述|默认|
|:-----------------------------------|:-----------------------------------------------|:--------------|
|`remote`|远程配置|`{}`|
|`remote.instances`|远程实例列表|必需 `[]`|
|`remote.instances.endpoint-prefix`|所有端点名称的前缀字符串|`""`|
|`remote.instances.url`|从中检索端点状态的 URL|必需 `""`|
|`remote.client`|[客户端配置](#client-configuration)。|`{}`|

```yaml
remote:
  instances:
    - endpoint-prefix: "status.example.org-"
      url: "https://status.example.org/api/v1/endpoints/statuses"
```


<a id="deployment"></a>
## 部署
许多示例可以在 [.examples](.examples) 文件夹中找到，但本节将重点介绍部署 Gatus 的最流行的方法。


<a id="docker"></a>
### Docker
要使用 Docker 在本地运行 Gatus：
```console
docker run -p 8080:8080 --name gatus ghcr.io/twin/gatus:stable
```

除了使用 [.examples](.examples) 文件夹中提供的示例之一之外，您还可以通过以下方式在本地尝试
创建一个配置文件，在本例中我们将其命名为 `config.yaml`，然后运行以下命令
命令：
```console
docker run -p 8080:8080 --mount type=bind,source="$(pwd)"/config.yaml,target=/config/config.yaml --name gatus ghcr.io/twin/gatus:stable
```

如果您使用的是 Windows，请将 `"$(pwd)"` 替换为当前目录的绝对路径，例如：
```console
docker run -p 8080:8080 --mount type=bind,source=C:/Users/Chris/Desktop/config.yaml,target=/config/config.yaml --name gatus ghcr.io/twin/gatus:stable
```

在本地构建镜像：
```console
docker build . -t ghcr.io/twin/gatus:stable
```


<a id="helm-chart"></a>
### Helm Chart
必须安装 [Helm](https://helm.sh) 才能使用图表。
请参考Helm的[文档](https://helm.sh/docs/)开始使用。

正确设置 Helm 后，添加存储库，如下所示：

```console
helm repo add twin https://twin.github.io/helm-charts
helm repo update
helm install gatus twin/gatus
```

要了解更多详细信息，请查看[图表配置](https://github.com/TwiN/helm-charts/blob/master/charts/gatus/README.md)。


<a id="terraform"></a>
### Terraform

<a id="kubernetes"></a>
#### 库伯内斯

可以使用 Terraform 通过以下模块将 Gatus 部署在 Kubernetes 上：[terraform-kubernetes-gatus](https://github.com/TwiN/terraform-kubernetes-gatus)。

<a id="running-the-tests"></a>
## 运行测试
```console
go test -v ./...
```


<a id="using-in-production"></a>
## 在生产中使用
请参阅[部署](#deployment) 部分。


<a id="faq"></a>
## 常问问题

<a id="sending-a-graphql-request"></a>
### 发送 GraphQL 请求
通过将 `endpoints[].graphql` 设置为 true，主体将自动由标准 GraphQL `query` 参数包裹。

例如，以下配置：
```yaml
endpoints:
  - name: filter-users-by-gender
    url: http://localhost:8080/playground
    method: POST
    graphql: true
    body: |
      {
        users(gender: "female") {
          id
          name
          gender
          avatar
        }
      }
    conditions:
      - "[STATUS] == 200"
      - "[BODY].data.users[0].gender == female"
```

将向 `http://localhost:8080/playground` 发送 `POST` 请求，其正文如下：
```json
{"query":"      {\n        users(gender: \"female\") {\n          id\n          name\n          gender\n          avatar\n        }\n      }"}
```


<a id="recommended-interval"></a>
### 推荐间隔
为了确保 Gatus 提供可靠且准确的结果（即响应时间），Gatus 限制了
可以同时评估的端点/套件。
换句话说，即使您有多个具有相同间隔的端点，也不能保证它们同时运行。

并发评估的数量由 `concurrency` 配置参数确定，默认为 `3`。

您可以通过运行 Gatus 来自己测试这一点，并使用配置了非常短、不切实际的间隔的多个端点，
比如1ms。您会注意到响应时间不会波动 - 这是因为在评估端点时
在不同的 goroutine 中，有一个信号量可以控制同时运行的端点/套件数量。

不幸的是，有一个缺点。如果您有很多端点，包括一些非常慢或容易超时的端点
（默认超时为 10 秒），这些缓慢的评估可能会阻止其他端点/套件的评估。

该间隔不包括请求本身的持续时间，这意味着如果一个端点的间隔为30s
并且请求需要 2 秒才能完成，两次评估之间的时间戳将是 32 秒，而不是 30 秒。

虽然这不会阻止 Gatus 对所有其他端点执行运行状况检查，但可能会导致 Gatus 无法
遵守配置的间隔，例如，假设 `concurrency` 设置为 `1`：
- 端点A间隔5s，10s后超时完成
- 端点B间隔5s，需要1ms完成
- 端点 B 将无法每 5 秒运行一次，因为端点 A 的健康评估时间比其间隔时间长

总而言之，虽然 Gatus 可以处理您输入的任何间隔，但您最好不要使用缓慢的请求
更高的间隔。

根据经验，我个人将更复杂的运行状况检查的时间间隔设置为 `5m`（5 分钟），
用于向 `30s` 发出告警 (PagerDuty/Twilio) 的简单运行状况检查。


<a id="default-timeouts"></a>
### 默认超时
|端点类型|暂停|
|:--------------|:--------|
|HTTP协议|10秒|
|传输控制协议|10秒|
|ICMP|10秒|

要修改超时，请参阅[客户端配置](#client-configuration)。


<a id="monitoring-a-tcp-endpoint"></a>
### 监控 TCP 端点
通过在 `endpoints[].url` 前面加上 `tcp://` 前缀，您可以在非常基本的级别上监视 TCP 端点：
```yaml
endpoints:
  - name: redis
    url: "tcp://127.0.0.1:6379"
    interval: 30s
    conditions:
      - "[CONNECTED] == true"
```
如果设置了 `endpoints[].body`，则发送该消息并且响应的前 1024 个字节将位于 `[BODY]` 中。

占位符 `[STATUS]` 以及字段 `endpoints[].headers`，
TCP 端点不支持 `endpoints[].method` 和 `endpoints[].graphql`。

这适用于数据库（Postgres、MySQL 等）和缓存（Redis、Memcached 等）等应用程序。

> 📝 `[CONNECTED] == true` 不保证端点本身是健康的 - 它只保证有
> 给定地址处的某些内容侦听给定端口，并且已成功连接到该地址
> 已确立的。


<a id="monitoring-a-udp-endpoint"></a>
### 监控 UDP 端点
通过在 `endpoints[].url` 前面加上 `udp://` 前缀，您可以在非常基本的级别上监视 UDP 端点：
```yaml
endpoints:
  - name: example
    url: "udp://example.org:80"
    conditions:
      - "[CONNECTED] == true"
```

如果设置了 `endpoints[].body`，则发送该消息并且响应的前 1024 个字节将位于 `[BODY]` 中。

占位符 `[STATUS]` 以及字段 `endpoints[].headers`，
UDP 端点不支持 `endpoints[].method` 和 `endpoints[].graphql`。

这适用于基于 UDP 的应用程序。


<a id="monitoring-a-sctp-endpoint"></a>
### 监控 SCTP 端点
通过在 `endpoints[].url` 上加上 `sctp://` 前缀，您可以在非常基本的级别上监控流控制传输协议 (SCTP) 端点：
```yaml
endpoints:
  - name: example
    url: "sctp://127.0.0.1:38412"
    conditions:
      - "[CONNECTED] == true"
```

占位符 `[STATUS]` 和 `[BODY]` 以及字段 `endpoints[].body`、`endpoints[].headers`、
SCTP 端点不支持 `endpoints[].method` 和 `endpoints[].graphql`。

这适用于基于 SCTP 的应用程序。


<a id="monitoring-a-websocket-endpoint"></a>
### 监控 WebSocket 端点
通过在 `endpoints[].url` 前面加上 `ws://` 或 `wss://` 前缀，您可以监控 WebSocket 端点：
```yaml
endpoints:
  - name: example
    url: "wss://echo.websocket.org/"
    body: "status"
    conditions:
      - "[CONNECTED] == true"
      - "[BODY] == pat(*served by*)"
```

`[BODY]` 占位符包含查询的输出，而 `[CONNECTED]`
显示连接是否成功建立。您可以使用Go模板
句法。


<a id="monitoring-an-endpoint-using-grpc"></a>
### 使用 gRPC 监控端点
您可以通过在 `endpoints[].url` 前面加上 `grpc://` 或 `grpcs://` 前缀来监控 gRPC 服务。
Gatus 针对目标执行标准 `grpc.health.v1.Health/Check` RPC。

```yaml
endpoints:
  - name: my-grpc
    url: grpc://localhost:50051
    interval: 30s
    conditions:
      - "[CONNECTED] == true"
      - "[BODY].status == SERVING"  # BODY is read only when referenced
    client:
      timeout: 5s
```

对于启用 TLS 的服务器，请使用 `grpcs://` 并根据需要配置客户端 TLS：

```yaml
endpoints:
  - name: my-grpcs
    url: grpcs://example.com:443
    conditions:
      - "[CONNECTED] == true"
      - "[BODY].status == SERVING"
    client:
      timeout: 5s
      insecure: false          # set true to skip cert verification (not recommended)
      tls:
        certificate-file: /path/to/cert.pem      # optional mTLS client cert
        private-key-file: /path/to/key.pem       # optional mTLS client key
```

笔记：
- 运行状况检查针对默认服务 (`service: ""`)。如果需要，可以稍后添加对自定义服务名称的支持。
- 仅当条件或套件存储映射需要时，响应正文才会公开为最小 JSON 对象，例如 `{"status":"SERVING"}`。
- 超时、自定义 DNS 解析器和 SSH 隧道通过现有的 [`client` 配置](#client-configuration) 实现。


<a id="monitoring-an-endpoint-using-icmp"></a>
### 使用 ICMP 监控端点
通过在 `endpoints[].url` 上添加 `icmp://` 前缀，您可以使用 ICMP 或更多功能在非常基本的级别上监视端点
通常称为“ping”或“echo”：
```yaml
endpoints:
  - name: ping-example
    url: "icmp://example.com"
    conditions:
      - "[CONNECTED] == true"
```

ICMP 类型的端点仅支持占位符 `[CONNECTED]`、`[IP]` 和 `[RESPONSE_TIME]`。
您可以指定以 `icmp://` 为前缀的域，或以 `icmp://` 为前缀的 IP 地址。

如果您在 Linux 上运行 Gatus，请阅读 [https://github.com/prometheus-community/pro-bing#linux]
如果您遇到任何问题。

在 `v5.31.0` 之前，某些环境设置需要添加 `CAP_NET_RAW` 功能才能允许 ping 工作。
从 `v5.31.0` 开始，这不再是必要的，除非以 root 身份运行，否则 ICMP 检查将适用于非特权 ping。有关详细信息，请参阅#1346。


<a id="monitoring-an-endpoint-using-dns-queries"></a>
### 使用 DNS 查询监控端点
在端点中定义 `dns` 配置会自动将所述端点标记为 DNS 类型的端点：
```yaml
endpoints:
  - name: example-dns-query
    url: "8.8.8.8" # Address of the DNS server to use
    dns:
      query-name: "example.com"
      query-type: "A"
    conditions:
      - "[BODY] == 93.184.215.14"
      - "[DNS_RCODE] == NOERROR"
```

有两个占位符可用于 DNS 类型端点的条件：
- 占位符 `[BODY]` 解析为查询的输出。例如，`A` 类型的查询将返回 IPv4。
- 占位符 `[DNS_RCODE]` 解析为与查询返回的响应代码关联的名称，例如
`NOERROR`、`FORMERR`、`SERVFAIL`、`NXDOMAIN` 等


<a id="monitoring-an-endpoint-using-ssh"></a>
### 使用 SSH 监控端点
您可以通过在 `endpoints[].url` 前面加上 `ssh://` 前缀来使用 SSH 监控端点：
```yaml
endpoints:
  # Password-based SSH example
  - name: ssh-example-password
    url: "ssh://example.com:22" # port is optional. Default is 22.
    ssh:
      username: "username"
      password: "password"
    body: |
      {
        "command": "echo '{\"memory\": {\"used\": 512}}'"
      }
    interval: 1m
    conditions:
      - "[CONNECTED] == true"
      - "[STATUS] == 0"
      - "[BODY].memory.used > 500"

  # Key-based SSH example
  - name: ssh-example-key
    url: "ssh://example.com:22" # port is optional. Default is 22.
    ssh:
      username: "username"
      private-key: |
        -----BEGIN RSA PRIVATE KEY-----
        TESTRSAKEY...
        -----END RSA PRIVATE KEY-----
    interval: 1m
    conditions:
      - "[CONNECTED] == true"
      - "[STATUS] == 0"
```

您还可以通过不指定用户名来使用无身份验证来监视端点，
密码和私钥字段。

```yaml
endpoints:
  - name: ssh-example
    url: "ssh://example.com:22" # port is optional. Default is 22.
    ssh:
      username: ""
      password: ""
      private-key: ""

    interval: 1m
    conditions:
      - "[CONNECTED] == true"
      - "[STATUS] == 0"
```

SSH 类型的端点支持以下占位符：
- 如果 SSH 连接成功，则 `[CONNECTED]` 解析为 `true`，否则解析为 `false`
- `[STATUS]` 解析在远程服务器上执行的命令的退出代码（例如 `0` 表示成功）
- `[BODY]` 解析为在远程服务器上执行的命令的 stdout 输出
- `[IP]` 解析为服务器的IP地址
- `[RESPONSE_TIME]` 解析为建立连接和执行命令所花费的时间


<a id="monitoring-an-endpoint-using-starttls"></a>
### 使用 STARTTLS 监控端点
如果您想要确保没有问题的电子邮件服务器，请通过 STARTTLS 对其进行监控
将作为一个很好的初始指标：
```yaml
endpoints:
  - name: starttls-smtp-example
    url: "starttls://smtp.gmail.com:587"
    interval: 30m
    client:
      timeout: 5s
    conditions:
      - "[CONNECTED] == true"
      - "[CERTIFICATE_EXPIRATION] > 48h"
```


<a id="monitoring-an-endpoint-using-tls"></a>
### 使用 TLS 监控端点
使用 SSL/TLS 加密（例如基于 TLS 的 LDAP）监控端点可以帮助检测证书过期：
```yaml
endpoints:
  - name: tls-ldaps-example
    url: "tls://ldap.example.com:636"
    interval: 30m
    client:
      timeout: 5s
    conditions:
      - "[CONNECTED] == true"
      - "[CERTIFICATE_EXPIRATION] > 48h"
```

如果设置了 `endpoints[].body`，则发送该消息并且响应的前 1024 个字节将位于 `[BODY]` 中。

占位符 `[STATUS]` 以及字段 `endpoints[].headers`，
TLS 端点不支持 `endpoints[].method` 和 `endpoints[].graphql`。


<a id="monitoring-domain-expiration"></a>
### 监控域名过期
您可以使用 `[DOMAIN_EXPIRATION]` 监控除 DNS 之外的所有端点类型的域的过期情况
占位符：
```yaml
endpoints:
  - name: check-domain-and-certificate-expiration
    url: "https://example.org"
    interval: 1h
    conditions:
      - "[DOMAIN_EXPIRATION] > 720h"
      - "[CERTIFICATE_EXPIRATION] > 240h"
```

> ⚠ 使用 `[DOMAIN_EXPIRATION]` 占位符需要 Gatus 使用 RDAP，或者作为后备方案，向官方 IANA WHOIS 服务发送请求
> [通过库](https://github.com/TwiN/whois)，在某些情况下，向特定于 TLD 的 WHOIS 服务器发出二次请求（例如 `whois.nic.sh`）。
> 为了防止 WHOIS 服务在您发送过多请求时限制您的 IP 地址，Gatus 将阻止您
> 在间隔小于 `5m` 的端点上使用 `[DOMAIN_EXPIRATION]` 占位符。


<a id="concurrency"></a>
### 并发性
默认情况下，Gatus 允许同时监控最多 3 个端点/套件。这提供了性能和资源使用之间的平衡，同时保持准确的响应时间测量。

您可以使用 `concurrency` 参数配置并发级别：

```yaml
# Allow 10 endpoints/suites to be monitored concurrently
concurrency: 10

# Allow unlimited concurrent monitoring
concurrency: 0

# Use default concurrency (3)
# concurrency: 3
```

**重要考虑因素：**
- 当您有许多端点时，更高的并发性可以提高监控性能
- 由于系统资源争用，使用 `[RESPONSE_TIME]` 占位符的条件在并发性非常高的情况下可能不太准确
- 设置为 `0` 以实现无限并发（相当于已弃用的 `disable-monitoring-lock: true`）

**更高并发的用例：**
- 您有大量端点需要监控
- 您希望以非常短的时间间隔（< 5s）监控端点
- 您正在使用 Gatus 进行负载测试场景

**旧配置：**
`disable-monitoring-lock` 参数已弃用，但仍受支持以实现向后兼容性。相当于设置`concurrency: 0`。


<a id="reloading-configuration-on-the-fly"></a>
### 即时重新加载配置
为了方便起见，如果加载的配置文件，Gatus 会自动重新加载配置
当 Gatus 运行时更新。

默认情况下，如果更新配置无效，应用程序将退出，但您可以配置
如果配置文件被更新为无效配置，Gatus 将继续运行
将 `skip-invalid-config-update` 设置为 `true`。

请记住，每次更新后确保配置文件的有效性符合您的最佳利益。
在 Gatus 运行时应用配置文件，方法是查看日志并确保您没有看到
以下消息：
```
The configuration file was updated, but it is not valid. The old configuration will continue being used.
```
如果不这样做，无论出于何种原因重新启动应用程序，Gatus 都可能无法启动。

我建议不要将 `skip-invalid-config-update` 设置为 `true` 以避免出现这种情况，但选择权在您
使.

**如果您不使用文件存储**，在 Gatus 运行时更新配置是有效的
与重新启动应用程序相同。

> 📝 如果绑定的是配置文件而不是配置文件夹，则可能无法检测到更新。请参阅 [#151](https://github.com/TwiN/gatus/issues/151)。


<a id="endpoint-groups"></a>
### 端点组
端点组用于将仪表板上的多个端点分组在一起。

```yaml
endpoints:
  - name: frontend
    group: core
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"

  - name: backend
    group: core
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"

  - name: monitoring
    group: internal
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"

  - name: nas
    group: internal
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"

  - name: random endpoint that is not part of a group
    url: "https://example.org/"
    interval: 5m
    conditions:
      - "[STATUS] == 200"
```

上面的配置将产生按组排序时如下所示的仪表板：

![Gatus 端点组](.github/assets/endpoint-groups.jpg)


<a id="how-do-i-sort-by-group-by-default"></a>
### 默认情况下如何按组排序？
在配置文件中将 `ui.default-sort-by` 设置为 `group`：
```yaml
ui:
  default-sort-by: group
```
请注意，如果用户已经按不同字段对仪表板进行排序，则不会应用默认排序，除非用户
清除浏览器的本地存储。


<a id="exposing-gatus-on-a-custom-path"></a>
### 在自定义路径上公开 Gatus
目前，您可以使用完全限定域名 (FQDN)（例如 `status.example.org`）公开 Gatus UI。但是，它不支持基于路径的路由，这意味着您无法通过像 `example.org/status/` 这样的 URL 公开它。

有关详细信息，请参阅 https://github.com/TwiN/gatus/issues/88.


<a id="exposing-gatus-on-a-custom-port"></a>
### 在自定义端口上公开 Gatus
默认情况下，Gatus 在端口 `8080` 上公开，但您可以通过设置 `web.port` 参数来指定不同的端口：
```yaml
web:
  port: 8081
```

如果您使用像 Heroku 这样的 PaaS，它不允许您设置自定义端口并通过环境公开它
变量请参阅[在配置文件中使用环境变量](#use-environment-variables-in-config-files)。

<a id="use-environment-variables-in-config-files"></a>
### 在配置文件中使用环境变量

您可以直接在配置文件中使用环境变量，该变量将从环境中替换：
```yaml
web:
  port: ${PORT}

ui:
  title: $TITLE
```
⚠️ 当您的配置参数包含 `$` 符号时，您必须使用 `$$` 转义 `$`。

<a id="configuring-a-startup-delay"></a>
### 配置启动延迟
如果出于任何原因，您需要 Gatus 在监视应用程序启动时的端点之前等待给定的时间，则可以使用 `GATUS_DELAY_START_SECONDS` 环境变量使 Gatus 在启动时休眠。


<a id="keeping-your-configuration-small"></a>
### 保持较小的配置
虽然不是特定于 Gatus，但您可以利用 YAML 锚点来创建默认配置。
如果您有一个很大的配置文件，这应该可以帮助您保持干净。

<details>
<summary>示例</summary>

```yaml
default-endpoint: &defaults
  group: core
  interval: 5m
  client:
    insecure: true
    timeout: 30s
  conditions:
    - "[STATUS] == 200"

endpoints:
  - name: anchor-example-1
    <<: *defaults               # This will merge the configuration under &defaults with this endpoint
    url: "https://example.org"

  - name: anchor-example-2
    <<: *defaults
    group: example              # This will override the group defined in &defaults
    url: "https://example.com"

  - name: anchor-example-3
    <<: *defaults
    url: "https://twin.sh/health"
    conditions:                # This will override the conditions defined in &defaults
      - "[STATUS] == 200"
      - "[BODY].status == UP"
```
</details>


<a id="proxy-client-configuration"></a>
### 代理客户端配置
您可以通过在客户端配置中设置 `proxy-url` 参数来配置客户端使用的代理。

```yaml
endpoints:
  - name: website
    url: "https://twin.sh/health"
    client:
      proxy-url: http://proxy.example.com:8080
    conditions:
      - "[STATUS] == 200"
```


<a id="how-to-fix-431-request-header-fields-too-large-error"></a>
### 如何修复 431 请求标头字段太大错误
根据您的环境部署位置以及 Gatus 前面的中间件或反向代理类型，
你可能会遇到这个问题。这可能是因为请求标头太大，例如大饼干。

默认情况下，`web.read-buffer-size` 设置为 `8192`，但像这样增加该值将增加读取缓冲区大小：
```yaml
web:
  read-buffer-size: 32768
```

<a id="badges"></a>
### 徽章

<a id="uptime"></a>
#### 正常运行时间
![正常运行时间 1 小时](https://status.twin.sh/api/v1/endpoints/core_blog-external/uptimes/1h/badge.svg)
![正常运行时间 24 小时](https://status.twin.sh/api/v1/endpoints/core_blog-external/uptimes/24h/badge.svg)
![正常运行时间 7 天](https://status.twin.sh/api/v1/endpoints/core_blog-external/uptimes/7d/badge.svg)
![正常运行时间 30 天](https://status.twin.sh/api/v1/endpoints/core_blog-external/uptimes/30d/badge.svg)

Gatus 可以为您的受监控端点之一自动生成 SVG 徽章。
这允许您将徽章放入各个应用程序的自述文件中，甚至创建您自己的状态页面（如果您愿意）
欲望。

生成徽章的路径如下：
```
/api/v1/endpoints/{key}/uptimes/{duration}/badge.svg
```
在哪里：
- `{duration}` 是 `30d`、`7d`、`24h` 或 `1h`
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。

例如，如果您想要过去 24 小时内来自组 `core` 中的端点 `frontend` 的正常运行时间，
URL 将如下所示：
```
https://example.com/api/v1/endpoints/core_frontend/uptimes/7d/badge.svg
```
如果要显示不属于组的端点，则必须将组值留空：
```
https://example.com/api/v1/endpoints/_frontend/uptimes/7d/badge.svg
```
例子：
```
![Uptime 24h](https://status.twin.sh/api/v1/endpoints/core_blog-external/uptimes/24h/badge.svg)
```
如果您想查看每个可用徽章的视觉示例，只需导航到端点的详细信息页面即可。


<a id="health"></a>
#### 健康
![健康](https://status.twin.sh/api/v1/endpoints/core_blog-external/health/badge.svg)

生成徽章的路径如下：
```
/api/v1/endpoints/{key}/health/badge.svg
```
在哪里：
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。

例如，如果您想要组 `core` 中端点 `frontend` 的当前状态，
URL 将如下所示：
```
https://example.com/api/v1/endpoints/core_frontend/health/badge.svg
```


<a id="health-shieldsio"></a>
#### 健康 (Shields.io)
![健康](https://img.shields.io/endpoint?url=https%3A%2F%2Fstatus.twin.sh%2Fapi%2Fv1%2Fendpoints%2Fcore_blog-external%2Fhealth%2Fbadge.shields)

生成徽章的路径如下：
```
/api/v1/endpoints/{key}/health/badge.shields
```
在哪里：
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。

例如，如果您想要组 `core` 中端点 `frontend` 的当前状态，
URL 将如下所示：
```
https://example.com/api/v1/endpoints/core_frontend/health/badge.shields
```

查看有关 Shields.io 徽章端点的更多信息[此处](https://shields.io/badges/endpoint-badge)。


<a id="response-time"></a>
#### 响应时间
![响应时间1小时](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/1h/badge.svg)
![响应时间24小时](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/24h/badge.svg)
![响应时间7d](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/7d/badge.svg)
![响应时间30d](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/30d/badge.svg)

生成徽章的端点如下：
```
/api/v1/endpoints/{key}/response-times/{duration}/badge.svg
```
在哪里：
- `{duration}` 是 `30d`、`7d`、`24h` 或 `1h`
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。

<a id="response-time-chart"></a>
#### 响应时间（图表）
![响应时间24小时](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/24h/chart.svg)
![响应时间7d](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/7d/chart.svg)
![响应时间30d](https://status.twin.sh/api/v1/endpoints/core_blog-external/response-times/30d/chart.svg)

生成响应时间图表的端点如下：
```
/api/v1/endpoints/{key}/response-times/{duration}/chart.svg
```
在哪里：
- `{duration}` 是 `30d`、`7d` 或 `24h`
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。

<a id="how-to-change-the-color-thresholds-of-the-response-time-badge"></a>
##### 如何更改响应时间徽章的颜色阈值
要更改响应时间标志的阈值，可以将相应的配置添加到端点。
数组中的值对应于级别 [Awesome、Great、Good、Passable、Bad]
所有五个值必须以毫秒 (ms) 为单位给出。

```yaml
endpoints:
- name: nas
  group: internal
  url: "https://example.org/"
  interval: 5m
  conditions:
    - "[STATUS] == 200"
  ui:
    badge:
      response-time:
        thresholds: [550, 850, 1350, 1650, 1750]
```


<a id="api"></a>
### 应用程序编程接口
Gatus 提供了一个简单的只读 API，可以查询该 API，以便以编程方式确定端点状态和历史记录。

所有端点都可以通过向以下端点发出 GET 请求来获得：
```
/api/v1/endpoints/statuses
````
示例：https://status.twin.sh/api/v1/endpoints/statuses

还可以使用以下模式查询特定端点：
```
/api/v1/endpoints/{group}_{endpoint}/statuses
```
示例：https://status.twin.sh/api/v1/endpoints/core_blog-home/statuses

如果 `Accept-Encoding` HTTP 标头包含 `gzip`，则将使用 Gzip 压缩。

API 将返回一个 JSON 负载，其中 `Content-Type` 响应标头设置为 `application/json`。
查询 API 不需要这样的标头。


<a id="interacting-with-the-api-programmatically"></a>
#### 以编程方式与 API 交互
请参阅 [TwiN/gatus-sdk](https://github.com/TwiN/gatus-sdk)


<a id="raw-data"></a>
#### 原始数据
Gatus 公开受监控端点之一的原始数据。
这允许您在自己的应用程序中跟踪和聚合受监控端点的数据。例如，如果您想要跟踪超过 7 天的正常运行时间。

<a id="uptime"></a>
##### 正常运行时间
获取端点的原始正常运行时间数据的路径是：
```
/api/v1/endpoints/{key}/uptimes/{duration}
```
在哪里：
- `{duration}` 是 `30d`、`7d`、`24h` 或 `1h`
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。

例如，如果您想要来自 `core` 组中的端点 `frontend` 的过去 24 小时的原始正常运行时间数据，则 URL 将如下所示：
```
https://example.com/api/v1/endpoints/core_frontend/uptimes/24h
```

<a id="response-time"></a>
##### 响应时间
获取端点的原始响应时间数据的路径是：
```
/api/v1/endpoints/{key}/response-times/{duration}
```
在哪里：
- `{duration}` 是 `30d`、`7d`、`24h` 或 `1h`
- `{key}` 的模式为 `<GROUP_NAME>_<ENDPOINT_NAME>`，其中两个变量均为 ` `、`/`、`_`、`,`、`.`、`#`、`+` 和`&` 替换为 `-`。

例如，如果您想要来自组 `core` 中的端点 `frontend` 的过去 24 小时的原始响应时间数据，则 URL 将如下所示：
```
https://example.com/api/v1/endpoints/core_frontend/response-times/24h
```


<a id="installing-as-binary"></a>
### 作为二进制安装
您可以使用以下命令将 Gatus 下载为二进制文件：
```
go install github.com/TwiN/gatus/v5@latest
```


<a id="high-level-design-overview"></a>
### 高层设计概述
![Gatus 图](.github/assets/gatus-diagram.jpg)
