# Streaming

[Streaming](https://en.wikipedia.org/wiki/Streaming_media) is the process of transmitting audio and video data in a continuous flow over a wired or wireless internet connection.

## Index

* [Applications](#applications)
* [Media Servers](#media-servers)
* [Codecs](#codecs)
  * [AVC/H.264](#avch264)
  * [HEVC/H.265](#hevch265)
* [Transport](#transport)
  * [RTP](#rtp)
  * [RTSP](#rtsp)
  * [RTMP](#rtmp)
  * [HLS](#hls)
  * [DASH](#dash)
  * [SRT](#srt)
  * [NDI](#ndi)
* [Topologies](#topologies)
  * [Mesh](#mesh)
  * [MCU](#mcu)
  * [SFU](#sfu)
* [Synchronization](#synchronization)
* [Bandwidth Strategies](#bandwidth-strategies)
  * [Simulcast](#simulcast)
  * [Scalable Video Coding](#scalable-video-coding)
* [References](#references)

## Applications

Streaming applications are software programs that allow users to reproduce streams or to stream content over the internet. These applications are designed to facilitate the transmission and playback of video data, making it easy for users to watch audiovisual content from anywhere with an internet connection.

There are many streaming applications available, including:
* [Open Broadcaster Software (OBS)](https://obsproject.com/)
* [VideoLan Media Player (VLC)](https://www.videolan.org/vlc/)
* [mpv](https://mpv.io/)

## Media Servers

[Media servers](https://en.wikipedia.org/wiki/Media_server) are software programs that deliver video and audio content to clients who request it. The most common use of media servers is to deliver [video on demand (VOD)](https://en.wikipedia.org/wiki/Video_on_demand), in which the media server retrieves prerecorded video content from storage and delivers it across the Internet. Live streaming media servers deliver content as it is generated in real time or with only a slight delay.

There are many streaming media servers available, including:
* [AntMedia](https://github.com/ant-media)
* [Broadcast Box](https://github.com/Glimesh/broadcast-box)
* [Janus](https://github.com/meetecho)
* [Jitsi](https://github.com/jitsi)
* [Kurento](https://github.com/Kurento/kurento-media-server)
* [LiveKit](https://github.com/livekit)
* [MediaMTX](https://github.com/aler9/mediamtx)
* [Medooze](https://github.com/medooze)
* [Millicast](https://www.millicast.com/)
* [Node Media Server](https://github.com/illuspas/Node-Media-Server)
* [Oven Media Engine](https://github.com/AirenSoft/OvenMediaEngine)
* [Simple Realtime Server](https://github.com/ossrs/srs)

## Codecs

[Codecs](https://en.wikipedia.org/wiki/Codec) are devices or computer programs which encode or decode data streams or signals. [Quantization](https://en.wikipedia.org/wiki/Quantization_(signal_processing)) is used to map input values from a large set (often a continuous set) to output values in a countable smaller set (often a finite set). The greater the quantization step, the lower the quality of the encoded video (lower [Peak signal-to-noise ratio (PSNR)](https://en.wikipedia.org/wiki/Peak_signal-to-noise_ratio)) the lower the bitrates. Greater quantization comes with lower computation complexity.

### AVC/H.264

[Advanced Video Coding (AVC)](https://en.wikipedia.org/wiki/Advanced_Video_Coding), also known as H.264, is a [video compression standard](https://en.wikipedia.org/wiki/Video_coding_format) based on block-oriented, [motion-compensated coding](https://en.wikipedia.org/wiki/Motion_compensation). Is the most commonly used format for the recording, compression, and distribution of video content but it is not well suited for the high bandwidth demands of 4K streaming due to the high compression ratios. It has many kinds of [profiles](https://en.wikipedia.org/wiki/Advanced_Video_Coding#Profiles) and [levels](https://en.wikipedia.org/wiki/Advanced_Video_Coding#Levels), and not every encoder or decoder supports every profile and level.

**profile-level-id**
* The first byte represents `profile_idc`.
* The second byte represents `profile_iop`. Each bit of it corresponds to `constraint_set{0,1,2,3,4,5}_flag`, a total of 6 bits, the last 2 bits are reserved bits, which are always 0.
* The third byte represents `level_idc`.

**Constrained Baseline**<br>
Decoders conforming to the `Constrained Baseline` profile at a specific level shall be capable of decoding all bitstreams in which all of the following are true:
* `profile_idc` is equal to 66 or constraint_set0_flag is equal to 1.
* `constraint_set1_flag` is equal to 1.
* `level_idc` and `constraint_set3_flag` represent a level less than or equal to the specified level.

**Examples**
* `0x42001f`
  * The first byte `0x42` (66) corresponds to profile `Baseline Profile`.
  * The third byte `0x1f` (31) corresponds to level `3.1`.
* `0x42e01f`
  * The first byte `0x42` (66) corresponds to profile `Baseline Profile`.
  * The second byte `0xe0` (1 1 1 0 0 0 00) matchs to `Constrained`.
  * The third byte `0x1f` (31) corresponds to level `3.1`.
* `0x4d0032`
  * The first byte `0x4d` (77) corresponds to profile `Main Profile`.
  * The third byte `0x32` (50) corresponds to level `5.0`.
* `0x640032`
  * The first byte `0x64` (100) corresponds to profile `High Profile`.
  * The third byte `0x32` (50) corresponds to level `5.0`.
* `0x640c34`
  * The first byte `0x64` (100) corresponds to profile `High Profile`.
  * The second byte `0x0c` matchs to `Constrained`.
  * The third byte `0x34` (52) corresponds to level `5.2`.

### HEVC/H.265

[High Efficiency Video Coding (HEVC)](https://en.wikipedia.org/wiki/High_Efficiency_Video_Coding), also known as H.265, is a video compression standard designed as a successor to the widely used [AVC](https://en.wikipedia.org/wiki/Advanced_Video_Coding). In comparison to AVC, HEVC offers from 25% to 50% better data compression at the same level of video quality, or substantially improved video quality at the same bit rate. It supports resolutions up to 8192x4320, including 8K UHD.

## Transport

Transport protocols are standardized methods of delivering different types of media over the internet. They send chunks of content from one endpoint to another and define the method for reassembling these chunks into playable content on the other endpoint.

### RTP

[Real-time Transport Protocol (RTP)](https://en.wikipedia.org/wiki/Real-time_Transport_Protocol) is a network protocol used in communication and entertainment systems that involve streaming media.

### RTSP

[Real Time Streaming Protocol (RTSP)](https://en.wikipedia.org/wiki/Real_Time_Streaming_Protocol) is an application-level network protocol designed for multiplexing and packetizing multimedia transport streams. The transmission of streaming data itself is not a task of RTSP, most media servers use [RTP](https://en.wikipedia.org/wiki/Real-time_Transport_Protocol) in conjunction with [RTCP](https://en.wikipedia.org/wiki/RTP_Control_Protocol) for media stream delivery. Clients of media servers issue commands such as play, record and pause, to facilitate real-time control of the media streaming. The well known TCP port for RTSP traffic is 554. The most common use case of RTSP is streaming using [IP cameras](https://en.wikipedia.org/wiki/IP_camera).

### RTMP

[Real-Time Messaging Protocol (RTMP)](https://en.wikipedia.org/wiki/Real-Time_Messaging_Protocol) is a communication protocol for streaming audio, video, and data over the Internet that works on top of TCP and uses port number 1935 by default.

### HLS

[HTTP Live Streaming (HLS)](https://en.wikipedia.org/wiki/HTTP_Live_Streaming) is an HTTP-based adaptive bitrate streaming communications protocol. Resembles [DASH](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP) in that it works by breaking the overall stream into a sequence of small HTTP-based file downloads, each downloading one short chunk of an overall potentially unbounded transport stream. A list of available streams, encoded at different bit rates, is sent to the client using an [extended M3U playlist](https://en.wikipedia.org/wiki/M3U).

### DASH

[Dynamic Adaptive Streaming over HTTP (DASH)](https://en.wikipedia.org/wiki/Dynamic_Adaptive_Streaming_over_HTTP), also known as MPEG-DASH, is an adaptive bitrate streaming technique that enables high quality streaming of media content over the Internet delivered from conventional HTTP web servers. Similar to [HLS](https://en.wikipedia.org/wiki/HTTP_Live_Streaming), DASH works by breaking the content into a sequence of small segments, which are served over HTTP.

### SRT

[Secure Reliable Transport (SRT)](https://en.wikipedia.org/wiki/Secure_Reliable_Transport) is an open source transport protocol that provides connection and control, reliable transmission at the application layer using UDP as the underlying transport layer. It supports packet recovery while maintaining low latency (120ms by default) and also supports encryption using AES.
It has 3 working modes:
* `Listener` runs a server to listen for incoming connections.
* `Caller` starts a connection to a known listener.
* `Rendezvous` creates a bi-directional link where the first to initiate handshake is considered caller.

### NDI

[Network Device Interface (NDI)](https://www.ndi.tv/) is a royalty-free software standard developed by NewTek to enable video-compatible products to communicate, deliver, and receive high-definition video over a computer network in a high-quality, low-latency manner that is frame accurate and suitable for switching in a live production environment.

## Topologies

### Mesh

In a mesh topology each node is directly connected to every other node. Each node sends its streams to every single node and downloads the streams from every node.

<p align="center"><img align="center" width="50%" height="50%" src="assets/mesh_topology.jpg"></p>

For a session with N nodes the total number of connections is `O(N²)`.

| Nodes                    | N      |
|--------------------------|--------|
| Uplinks                  | N(N-1) |
| Downlinks                | N(N-1) |
| Uplinks<sub>node</sub>   | N-1    |
| Downlinks<sub>node</sub> | N-1    |

✅ Pros:
* Low latency.
* Low server loads.
* End-to-end encryption.

❌ Cons:
* Poor scaling.
* High node loads.
* Connectivity problems with NATs, firewalls, etc.

### MCU

In a Multipoint Conferencing Unit (MCU) topology each node is connected to the MCU server. With a MCU, each node uploads its stream once, the server `decodes` the stream, mixes the streams of all the nodes into one and `encodes` the stream to send it back to each node.

<p align="center"><img align="center" width="50%" height="50%" src="assets/mcu_topology.jpg"></p>

For a session with N nodes the total number of connections is `O(N)`.

| Nodes                    | N |
|--------------------------|---|
| Uplinks                  | N |
| Downlinks                | N |
| Uplinks<sub>node</sub>   | 1 |
| Downlinks<sub>node</sub> | 1 |

✅ Pros:
* Good scaling.
* Low node loads.
* No connectivity problems.
* Works well in low bandwidth environments.

❌ Cons:
* High latency.
* High server loads.

### SFU

In a Selective Forwarding Unit (SFU) topology each node is connected to the SFU server. With a SFU, each node uploads its stream once and the server `forwards` the stream to every node.

<p align="center"><img align="center" width="50%" height="50%" src="assets/sfu_topology.jpg"></p>

For a session with N nodes the total number of connections is `O(N²)`.

| Nodes                    | N      |
|--------------------------|--------|
| Uplinks                  | N      |
| Downlinks                | N(N-1) |
| Uplinks<sub>node</sub>   | 1      |
| Downlinks<sub>node</sub> | N-1    |

✅ Pros:
* Good scaling.
* Medium node loads.
* Low server loads.
* No connectivity problems.

❌ Cons:
* No end-to-end encryption (although there are experimental approaches of header only decryption).

## Synchronization

Audio-video synchronization is critical in any multimedia system, especially in real-time streaming applications. Desynchronization (often called lip-sync error) is one of the most noticeable and annoying issues for users as a result of audio and video drifting out of sync and is caused by variable network delay and jitter, packet loss and retransmissions, or asynchronous decoding and buffering.

### 1. Timestamp-based

* <b>How</b>: Each audio and video frame includes a presentation timestamp (PTS). The playback system uses a common clock reference to schedule frame rendering.
* <b>Where</b>: MPEG or MP4 containers, WebRTC, RTSP, HLS, DASH, etc.
* <b>Requires</b>:
  * Accurate timestamps from the encoder or capture system.
  * A shared clock reference (e.g. NTP or wall clock).
* <b>Challenges</b>:
  * Network jitter can cause drift.
  * Need for jitter buffers and sync correction logic.

### 2. Audio as Master Clock

* <b>How</b>: Audio is played back as-is (because it’s more sensitive to glitches), and video is adjusted to follow it. Video frames are delayed, dropped, or repeated to match audio.
* <b>Why</b>: The human ear is more sensitive to timing discrepancies than the eye, especially for speech.
* <b>Where</b>:
  * Media players (VLC, ffplay, etc.).
  * Live streaming (WebRTC, OBS, etc.).

### 3. Video as Master Clock

* <b>How</b>: Audio is adjusted (usually by stretching or resampling) to match video timing.
* <b>Where</b>:
  * Less common, but can be used in video-dominant applications.
  * Video editing/rendering workflows where visual accuracy is more important.
* <b>Challenges</b>: Audio pitch and quality can be affected if resampling isn't handled carefully.

### 4. Global Master Clock

* <b>How</b>: Both audio and video streams sync to a shared system clock (e.g. NTP time, RTP clock, etc.).
* <b>Where</b>:
  * Broadcast systems.
  * WebRTC (via RTCP Sender Reports).
  * Distributed media systems (e.g. live concerts, multi-device sync, etc.).
* <b>Requires</b>: Clock drift compensation (if hardware clocks aren't perfectly synced).

### 5. Buffer-based

* <b>How</b>: Frames are placed into a jitter buffer to absorb network jitter (often combined with hysteresis logic), and playback waits until audio and video are close enough in time.
* <b>Challenges</b>: May introduce latency but improves stability.

### 6. Manual or Heuristic Adjustment

* <b>How</b>: The system monitors sync error (difference in timestamps) using thresholds and hysteresis, to avoid jittery behavior applies:
  * Frame dropping (to catch up).
  * Frame delaying (to wait for the other stream).
  * Dynamic audio resampling.
* <b>Where</b>: Used in custom synchronizers and playback engines.

Hysteresis is a concept from physics and control systems. It refers to situations where the response of a system depends on its past state, not just its current input. In software, hysteresis is often used to avoid constant state changes caused by small fluctuations, essentially to smooth out behavior. In the context of synchronizing audio and video over the internet, hysteresis is used to prevent jittery or overly sensitive corrections when there's a slight timing mismatch between audio and video frames.

When building a synchronization system, you often define a tolerance window where small differences between audio and video timestamps are considered close enough and no correction is made. The system will only apply a correction if the sync error goes beyond the allowed tolerance plus the hysteresis buffer.

Example:
* If the difference is less than 40 ms, the system does nothing.
* If the difference is greater than 60 ms, the system applies a correction (e.g. dropping or delaying frames).
* If the difference is between 40–60 ms, the system does nothing (this buffer zone is the hysteresis).
```py
SYNC_TOLERANCE = 0.04 # 40ms
SYNC_HYSTERESIS = 0.02 # 20ms

def should_correct_sync(sync_error):
    if abs(sync_error) > (SYNC_TOLERANCE + SYNC_HYSTERESIS):
        return True
    return False
```

Benefits:
* Avoids constantly correcting minor and temporary sync issues.
* Prevents visual instability caused by frequent adjustments.
* Reduces computational overhead from unnecessary resync operations.
* Provides a smoother user experience during streaming or playback.

### 7. RTCP Sender Reports (RTP)

* <b>How</b>: RTCP Sender Reports carry timestamps mapping RTP timestamps to NTP time. This allows aligning audio and video tracks that use different clocks.
* <b>Where</b>: In RTP-based streaming (e.g. WebRTC).

### 8. AV Interleaving in Media Containers

* <b>How</b>: Interleave audio and video packets where the demuxer ensures the decoder receives both in sync order.
* <b>Where</b>:
  * Stored media playback (not real-time).
  * Formats like MP4, MKV or MPEG-TS.

## Bandwidth Strategies

In video streaming, bandwidth usage directly impacts the resolution, clarity, and overall viewing experience. Higher resolutions like high definition (HD) or standard definition (SD) require more bandwidth for smooth playback than lower ones.

For example:
<br>
* A videoconference of 2 streams of 1920x1080 at 30fps, assuming a 3mbps bitrate.<br>
3/8 `(1MB/s = 8Mb/s)` * 60 `(seconds)` * 2 `(streams)` = 45MB/min

* A videoconference of 2 streams of 640x360 at 30fps, assuming a 1mbps bitrate.<br>
1/8 `(1MB/s = 8Mb/s)` * 60 `(seconds)` * 2 `(streams)` = 15MB/min

### Simulcast

Simulcast allows peers to publish multiple versions of the same stream with different **spatial** or **temporal** encodings, effectively sending more data.

#### Spatial

With spatial scalability the lower resolution layers consume less bandwidth than the high resolution ones.

For example:
* High: 1280x720 2.5mbps
* Medium: 640x360 400kbps
* Low: 320x180 125kbps

The peer uses just 17% more bandwidth to publish the three layers.

#### Temporal

With temporal scalability it is possible to lower a stream's bitrate by dynamically reducing the stream's frame rate. 

Streams contain mostly **delta** frames which depend on previous **key** frames. If the decoder needs to apply a delta to a key frame that was dropped, it can't render subsequent frames.

When temporal layers are used, frames from the base layer only reference other base layer frames.

<p align="center"><img align="center" width="70%" height="70%" src="assets/temporal_simulcast.png"></p>

For a subscriber with limited bandwidth, it is possible to send only the frames of a specific temporal layer, effectively reducing bandwidth.

### Scalable Video Coding

[Scalable Video Coding (SVC)](https://en.wikipedia.org/wiki/Scalable_Video_Coding) is a video compression standard that defines encoding of a high-quality video bitstream that also contains one or more subset bitstreams (a form of layered coding). A subset video bitstream is derived by dropping packets from the larger video to reduce the bandwidth required for the subset bitstream. The subset bitstream can represent a lower spatial resolution (smaller screen), lower temporal resolution (lower frame rate), or lower quality video signal.

## References

* [Digital Video Introduction](https://github.com/leandromoreira/digital_video_introduction)
* [IBM Internet connection and recommended encoding settings](https://support.video.ibm.com/hc/en-us/articles/207852117-Internet-connection-and-recommended-encoding-settings)
* [IBM Keyframes, Interframe and Video Compression](https://blog.video.ibm.com/streaming-video-tips/keyframes-interframe-video-compression/)
* [Twitch Broadcasting Guidelines](https://help.twitch.tv/s/article/broadcasting-guidelines/)
* [A Tale of Two Protocols: Comparing WebRTC against HLS for Live Streaming](https://blog.livekit.io/webrtc-vs-hls-livestreaming/)
* [iSpy Camera Connection Database](https://www.ispyconnect.com/cameras)
* [What is a Codec?](https://superuser.com/questions/300897/what-is-a-codec-e-g-divx-and-how-does-it-differ-from-a-file-format-e-g-mp)
