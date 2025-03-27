# LiveKit

<p align="center"><img align="center" width="20%" height="20%" src="assets/livekit.png"></p>

[LiveKit](https://livekit.io/) is an open source project that provides scalable, multi-user conferencing over WebRTC.

## Index

* [General](#general)
* [CLI](#cli)
* [Profiling](#profiling)

## General

The [documentation](https://docs.livekit.io/) has guides and API references for deployment, working with rooms, etc.

Deployment can be made using the official Docker [image](https://hub.docker.com/r/livekit/livekit-server). The server is configured using the `livekit.yaml` configuration file, a [sample](https://github.com/livekit/livekit/blob/master/config-sample.yaml) is available in the official [repository](https://github.com/livekit/livekit).

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

Start in development mode.
```
livekit-server --dev
```

Create a room join token.
```
LIVEKIT_KEYS="<key>: <secret>" ./livekit-server create-join-token --room <room> --identity <user>
```

## CLI

The [livekit-cli](https://github.com/livekit/livekit-cli) command-line interface can be used to access server APIs, create tokens, create and join rooms, generate test traffic, etc.

Create a token.
```
livekit-cli create-token \
    --api-key <key> --api-secret <secret> \
    --join --room <room> --identity <user> \
    --valid-for 24h
```

Simulate a test publisher.
```
livekit-cli join-room \
    --url <url> \
    --api-key <key> --api-secret <secret> \
    --room <room> --identity <user> \
    --publish-demo
```

Publish media files.
```
livekit-cli join-room \
    --room <room> --identity <user> \
    --publish path/to/video.ivf \
    --publish path/to/audio.ogg \
    --fps 23.98
```
* Note that it's important to match video framerate with the source to prevent out of sync issues.

Simulate audio room.
```
livekit-cli load-test \
    --url <url> \
    --api-key <key> --api-secret <secret> \
    --room <room> --audio-publishers 10 --subscribers 1000
```

Simulate large meeting.
```
livekit-cli load-test \
    --url <url> \
    --api-key <key> --api-secret <secret> \
    --room <room> --video-publishers 150 --subscribers 150
```

Simulate livestreaming.
```
livekit-cli load-test \
    --url <url> \
    --api-key <key> --api-secret <secret> \
    --room <room> --video-publishers 1 --subscribers 3000
```

## Profiling

* [Connection Test](https://livekit.io/connection-test)
* [Meet](https://meet.livekit.io/)
* [Benchmarking](https://docs.livekit.io/realtime/self-hosting/benchmark/)
