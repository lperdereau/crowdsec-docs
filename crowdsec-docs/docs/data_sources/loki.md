---
id: loki
title: Loki
---

This module allows the `Security Engine` to acquire logs from aggregation system, in one-shot and streaming mode.

## Configuration example

To monitor with a given LogQL query:

```yaml
mode: tail
source: loki
url: http://localhost:3100/
query: >
  {server="demo"}
```

Look at the [configuration parameters](#Parameters) to view all supported options.

## Parameters

### `url`

**Required**

Loki Query URL

### `query`

**Required**

Query to filter Loki logs with (LogQL)[https://grafana.com/docs/loki/latest/logql/]

### `mode`

`tail` or `cat`

Default: `tail`

### `auth`

Allow to configure Basic Auth (ie: if you protect your Loki with Nginx)

Object like:

```yaml
auth:
  username: foo
  password: bar
```

### `limit`

Limit of logs to read

Default: 100

### `since`

Only in `cat` mode.

Read logs since timestamp (e.g. 2013-01-02T13:23:37Z) or relative (e.g. 42m for 42 minutes).

## DSN and command-line

Loki datasource implements a very approximative DSN, as follows : `loki://<loki_url>?[args]`

Supported args are :

- `log_level` : set log level of module
- `since` : read logs since timestamp (e.g. 2013-01-02T13:23:37Z) or relative (e.g. 42m for 42 minutes)
- `ssl` : configure url to have https scheme
- `limit` : limit log entries returned

A 'pseudo DSN' must be provided:

```bash
crowdsec -type nginx -dsn 'loki://foo:bar@localhost:3100/?query={server="nginx"}'
```
