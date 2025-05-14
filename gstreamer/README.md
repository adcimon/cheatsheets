# GStreamer

<p align="center"><img align="center" src="assets/gstreamer.svg"></p>

[GStreamer](https://gstreamer.freedesktop.org/) is a library for constructing graphs of media-handling components.

## Index

* [General](#general)
* [Streaming](#streaming)
  * [RTMP](#rtmp)

## General

Launch a test pipeline.
```
gst-launch audiotestsrc ! audioconvert ! autoaudiosink
gst-launch videotestsrc ! videoconvert ! autovideosink
```

Print info about a plugin or element.
```
gst-inspect
gst-inspect -a
gst-inspect <plugin>
gst-inspect <element>
```

Detect the media format of a file.
```
gst-typefind <file>
```

Play audio or video.
```
gst-launch playbin uri=<file://path/to/file>
```

Use element properties.
```
gst-launch audiotestsrc wave=saw freq=880 ! audioconvert ! autoaudiosink
```

## Streaming

### RTMP

Publish a test stream.
```
gst-launch-1.0 \
  flvmux name=mux streamable=true ! rtmp2sink location="rtmps://brainstorm.rtmp.livekit.cloud/x/cby5QkiLg5rt" \
  audiotestsrc wave=sine-table ! audioconvert ! faac ! queue ! mux. \
  videotestsrc is-live=true ! video/x-raw,width=1280,height=720 ! videoconvert ! x264enc speed-preset=3 tune=zerolatency ! queue ! mux.
```
* `flvmux` collects both audio and video and multiplexes them into a format suitable for RTMP.
* `streamable=true` ensures the muxed stream can be sent immediately without requiring the whole file.
* `queue` avoid blocking when muxing parallel streams.
* `videoconvert` and `audioconvert` ensure compatible formats are fed into encoders.

Publish microphone and camera (Windows).
```
gst-launch-1.0 \
  flvmux name=mux streamable=true ! rtmp2sink location="rtmp://<ip>:1935/<application>/<stream_name>/<stream_key>" \
  wasapisrc ! audioconvert ! audioresample ! faac ! queue ! mux. \
  ksvideosrc ! video/x-raw,width=1280,height=720,framerate=30/1 ! videoconvert ! x264enc speed-preset=ultrafast tune=zerolatency ! queue ! mux.
```
* `wasapisrc` or `directsoundsrc` for audio.

Publish microphone and camera (Linux).
```
gst-launch-1.0 \
  flvmux name=mux streamable=true ! rtmp2sink location="rtmp://<ip>:1935/<application>/<stream_name>/<stream_key>" \
  pulsesrc device=default ! audioconvert ! audioresample ! faac ! queue ! mux. \
  v4l2src device=/dev/video0 ! video/x-raw,width=1280,height=720,framerate=30/1 ! videoconvert ! x264enc speed-preset=ultrafast tune=zerolatency ! queue ! mux.
```
* `pulsesrc device=default` captures from the default PulseAudio input (typically microphone).
* `v4l2src device=/dev/video0` captures from the first webcam device.

Publish microphone and camera (MacOS).
```
gst-launch-1.0 \
  flvmux name=mux streamable=true ! rtmp2sink location="rtmp://<ip>:1935/<application>/<stream_name>/<stream_key>" \
  osxaudiosrc ! audioconvert ! audioresample ! faac ! queue ! mux. \
  avfvideosrc ! video/x-raw,width=1280,height=720,framerate=30/1 ! videoconvert ! x264enc speed-preset=ultrafast tune=zerolatency ! queue ! mux.
```
