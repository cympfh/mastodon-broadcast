# Mastodon Broadcast (mcast)

## 概念図

```
Mastodon-Stream -> [Broadcast] -> Server1
                             +--> Server2
                             +--> Server3
```

## setup

### config.sh

Mastodon auth config

```bash
$ cat config.sh
SERVER=mstdn.jp
USERTOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### broadcast destinations

1 line = 1 url (API endpoint)

```bash
$ cat dest.list
http://localhost:8080/
http://localhost:8081/
http://localhost:8082/api/mastodon/stream
```

### data

Mastodon raw stream is like this

```bash

:thump
event: update
{"type": ....}
:thump
event: notification
{"type": ....}
:thump
:thump
```

`mcast` converts this and send data for each data

```bash
{"event_type": "thump"}
{"event_type": "update", "data": {"type": ...}}
{"event_type": "thump"}
{"event_type": "notification", "data": {"type": ...}}
{"event_type": "thump"}
{"event_type": "thump"}
```


## usage

```bash
bash ./mcast
```
