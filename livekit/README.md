# LiveKit

[LiveKit](https://livekit.io/) is an open source project that provides scalable, multi-user conferencing over WebRTC.

## Index

* [General](#general)
* [Profiling](#profiling)

## General

The [documentation](https://docs.livekit.io/) has guides and API references for deployment, working with rooms, etc.

Deployment can be made using the official [Docker image](https://hub.docker.com/r/livekit/livekit-server). The server is configured using the `livekit.yaml` configuration file, a [sample](https://github.com/livekit/livekit/blob/master/config-sample.yaml) is available in the [repository](https://github.com/livekit/livekit).

Example of `livekit.yaml`:
```
port: 7880
rtc:
    port_range_start: 50000
    port_range_end: 50200
    tcp_port: 7881
    use_external_ip: true
keys:
    <API_KEY>: <API_SECRET>
logging:
    json: false
    level: info
```

## Profiling

* [Connection Test](https://livekit.io/connection-test)
* [Playground](https://livekit.io/playground)
* [Example](https://example.livekit.io/)
