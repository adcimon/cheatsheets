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

Publish a stream (Windows).
```
gst-launch-1.0 \
  flvmux name=mux streamable=true ! rtmp2sink location="rtmp://<ip>:1935/<application>/<stream_name>/<stream_key>" \
  wasapisrc ! audioconvert ! audioresample ! faac ! queue ! mux. \
  ksvideosrc ! video/x-raw,width=1280,height=720,framerate=30/1 ! videoconvert ! x264enc speed-preset=ultrafast tune=zerolatency ! queue ! mux.
```
* `wasapisrc` or `directsoundsrc` for audio.

Publish a stream (Linux).
```
gst-launch-1.0 \
  flvmux name=mux streamable=true ! rtmp2sink location="rtmp://<ip>:1935/<application>/<stream_name>/<stream_key>" \
  pulsesrc device=default ! audioconvert ! audioresample ! faac ! queue ! mux. \
  v4l2src device=/dev/video0 ! video/x-raw,width=1280,height=720,framerate=30/1 ! videoconvert ! x264enc speed-preset=ultrafast tune=zerolatency ! queue ! mux.
```
* `pulsesrc device=default` captures from the default PulseAudio input (typically microphone).
* `v4l2src device=/dev/video0` captures from the first webcam device.
* `queue` separates threads and ensures smooth flow between elements.

Publish a stream (MacOS).
```
gst-launch-1.0 \
  flvmux name=mux streamable=true ! rtmp2sink location="rtmp://<ip>:1935/<application>/<stream_name>/<stream_key>" \
  osxaudiosrc ! audioconvert ! audioresample ! faac ! queue ! mux. \
  avfvideosrc ! video/x-raw,width=1280,height=720,framerate=30/1 ! videoconvert ! x264enc speed-preset=ultrafast tune=zerolatency ! queue ! mux.
```
