# WebRTC

<p align="center"><img align="center" src="webrtc.png"></p>

[WebRTC](https://webrtc.org/) is a free and open-source project providing web browsers and mobile applications with real-time peer-to-peer communications.

## Index

* [ICE](#ice)
* [Architectures](#architectures)
* [References](#references)

## ICE

[Interactive Connectivity Establishment (ICE)](https://en.wikipedia.org/wiki/Interactive_Connectivity_Establishment) is a protocol for [Network Address Translator (NAT)](https://en.wikipedia.org/wiki/Network_address_translation) traversal used in computer networking to find ways for two computers to talk to each other as directly as possible in [peer-to-peer](https://en.wikipedia.org/wiki/Peer-to-peer) networking.

* Address discovery using [Session Traversal Utilities for NAT (STUN)](https://en.wikipedia.org/wiki/STUN) protocol.
* Relay messages between two peers when direct traffic is not allowed using [Traversal Using Relays around NAT (TURN)](https://en.wikipedia.org/wiki/Traversal_Using_Relays_around_NAT) protocol.

## Architectures

### Simulcast

Simulcast allows peers to publish multiple versions of the same stream with different **spatial** or **temporal** encodings, effectively sending more data.

With **spatial** scalability the lower resolution layers consume less bandwidth than the high resolution ones. For example:
* High: 1280x720 2.5mbps
* Medium: 640x360 400kbps
* Low: 320x180 125kbps

The peer uses just 17% more bandwidth to publish the three layers.

With **temporal** scalability it is possible to lower a stream's bitrate by dynamically reducing the stream's frame rate. Streams contain mostly **delta** frames which depend on previous **key** frames. If the decoder needs to apply a delta to a key frame that was dropped, it can't render subsequent frames. When temporal layers are used only delta frames from one layer reference key frames from the same layer.

For a subscriber with limited bandwidth, it is possible to send only the frames of a temporal layer.

## References

* [WebRTC for the Curious](https://webrtcforthecurious.com/)
* [WebRTC Glossary](https://webrtcglossary.com/)
* [WebRTC API MDN](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API)
* [Troubleshooter](https://test.webrtc.org/)
* [Samples](https://webrtc.github.io/samples/)
* [Trickle ICE](https://webrtc.github.io/samples/src/content/peerconnection/trickle-ice/)
