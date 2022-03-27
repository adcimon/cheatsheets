# Streaming

[Streaming](https://en.wikipedia.org/wiki/Streaming_media) is the process of transmitting audio and video data in a continuous flow over a wired or wireless internet connection.

## Index

* [Topologies](#topologies)
  * [Mesh](#mesh)
  * [MCU](#mcu)
  * [SFU](#sfu)
* [Simulcast](#simulcast)
* [Scalable Video Coding](#scalable-video-coding)
* [References](#references)

## Topologies

### Mesh

In a mesh topology each node is directly connected to every other node. Each node sends its streams to every single node and downloads the streams from every node.

<p align="center"><img align="center" width="40%" height="40%" src="assets/mesh_topology.jpg"></p>

For a session with N nodes the total number of connections is `O(N²)`.

| Nodes                    | N      |
|--------------------------|--------|
| Uplinks                  | N(N-1) |
| Downlinks                | N(N-1) |
| Uplinks<sub>peer</sub>   | N-1    |
| Downlinks<sub>peer</sub> | N-1    |

Pros:
* Low latency.
* Low server loads.
* End-to-end encryption.

Cons:
* Poor scaling.
* High node loads.
* Connectivity problems with NATs, firewalls, etc.

### MCU

In a Multipoint Conferencing Unit (MCU) topology each node is connected to the MCU server. With a MCU, each node uploads its stream once, the server `decodes` the stream, mixes the streams of all the nodes into one and `encodes` the stream to send it back to each node.

<p align="center"><img align="center" width="40%" height="40%" src="assets/mcu_topology.jpg"></p>

For a session with N nodes the total number of connections is `O(N)`.

| Nodes                    | N |
|--------------------------|---|
| Uplinks                  | N |
| Downlinks                | N |
| Uplinks<sub>peer</sub>   | 1 |
| Downlinks<sub>peer</sub> | 1 |

Pros:
* Good scaling.
* Low node loads.
* No connectivity problems.
* Works well in low bandwidth environments.

Cons:
* High latency.
* High server loads.

### SFU

In a Selective Forwarding Unit (SFU) topology each node is connected to the SFU server. With a SFU, each node uploads its stream once and the server `forwards` the stream to every node.

<p align="center"><img align="center" width="40%" height="40%" src="assets/sfu_topology.jpg"></p>

For a session with N nodes the total number of connections is `O(N²)`.

| Nodes                    | N      |
|--------------------------|--------|
| Uplinks                  | N      |
| Downlinks                | N(N-1) |
| Uplinks<sub>peer</sub>   | 1      |
| Downlinks<sub>peer</sub> | N-1    |

Pros:
* Good scaling.
* Medium node loads.
* Low server loads.
* No connectivity problems.

Cons:
* No end-to-end encryption (although there are experimental approaches of header only decryption).

## Simulcast

Simulcast allows peers to publish multiple versions of the same stream with different **spatial** or **temporal** encodings, effectively sending more data.

### Spatial

With spatial scalability the lower resolution layers consume less bandwidth than the high resolution ones.

For example:
* High: 1280x720 2.5mbps
* Medium: 640x360 400kbps
* Low: 320x180 125kbps

The peer uses just 17% more bandwidth to publish the three layers.

### Temporal

With temporal scalability it is possible to lower a stream's bitrate by dynamically reducing the stream's frame rate. 

Streams contain mostly **delta** frames which depend on previous **key** frames. If the decoder needs to apply a delta to a key frame that was dropped, it can't render subsequent frames.

When temporal layers are used, frames from the base layer only reference other base layer frames.

<p align="center"><img align="center" width="60%" height="60%" src="assets/temporal_simulcast.png"></p>

For a subscriber with limited bandwidth, it is possible to send only the frames of a specific temporal layer, effectively reducing bandwidth.

## Scalable Video Coding

[Scalable Video Coding (SVC)](https://en.wikipedia.org/wiki/Scalable_Video_Coding) is a video compression standard that defines encoding of a high-quality video bitstream that also contains one or more subset bitstreams (a form of layered coding). A subset video bitstream is derived by dropping packets from the larger video to reduce the bandwidth required for the subset bitstream. The subset bitstream can represent a lower spatial resolution (smaller screen), lower temporal resolution (lower frame rate), or lower quality video signal.

## References

* [Internet connection and recommended encoding settings](https://support.video.ibm.com/hc/en-us/articles/207852117-Internet-connection-and-recommended-encoding-settings)
* [H.264 is Magic](https://sidbala.com/h-264-is-magic/)
