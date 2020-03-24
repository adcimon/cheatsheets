# GStreamer

[GStreamer](https://gstreamer.freedesktop.org/) is a library for constructing graphs of media-handling components.

Launch a test pipeline.
```
gst-launch audiotestsrc ! audioconvert ! autoaudiosink
gst-launch videotestsrc ! videoconvert ! autovideosink
```

Print info about a plugin or element.
```
gst-inspect
gst-inspect -a
gst-inspect plugin
gst-inspect element
```

Detect the media format of a file.
```
gst-typefind file
```

Play audio or video.
```
gst-launch playbin uri=file://path/to/file
```

Use element properties.
```
gst-launch audiotestsrc wave=saw freq=880 ! audioconvert ! autoaudiosink
```