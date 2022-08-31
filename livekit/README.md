# LiveKit

[LiveKit](https://github.com/livekit) is an open source project that provides scalable, multi-user conferencing over WebRTC.

## Index

* [General](#general)
* [Profiling](#profiling)

## General

LiveKit has a configuration file to deploy the server, a sample [config-sample.yaml](https://github.com/livekit/livekit/blob/master/config-sample.yaml) is provided in the repository.

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
* [Example](https://example.livekit.io/)
