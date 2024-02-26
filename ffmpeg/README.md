# FFmpeg

<p align="center"><img align="center" width="30%" height="30%" src="assets/ffmpeg.svg"></p>

[FFmpeg](https://www.ffmpeg.org/) is a complete, cross-platform solution to record, convert and stream audio and video.

## Index

* [General](#general)
* [Muxing](#muxing)
* [Transcoding](#transcoding)
  * [x264](#x264)
  * [NVENC/NVDEC](#nvencnvdec)
* [Editing](#editing)
  * [Trim](#trim)
  * [Loop](#loop)
  * [Speed Up/Slow Down](#speed-upslow-down)
  * [Delay](#delay)
  * [Volume](#volume)
  * [Rotate](#rotate)
  * [Scale](#scale)
  * [Slice](#slice)
  * [GIF](#gif)
  * [Draw](#draw)
  * [Metadata](#metadata)
* [Streaming](#streaming)
  * [RTP](#rtp)
  * [RTSP](#rtsp)
  * [RTMP](#rtmp)
  * [HLS](#hls)
  * [Dash](#dash)
  * [SRT](#srt)
  * [NDI](#ndi)
  * [Synchronization](#synchronization)
  * [Latency](#latency)
* [Devices](#devices)
  * [DirectShow](#directshow)
* [Options](#options)

## General

Check version.
```
ffmpeg -version
```

Convert audio and video.
```
ffmpeg -i <input> <output>
```
* [`-i`](https://ffmpeg.org/ffmpeg.html#Description) specifies the input files to read.

## Muxing

Remux a mkv into mp4.
```
ffmpeg -i input.mkv -c:a copy -c:v copy output.mp4
```

Mux the video from `input0` and audio from `input1` to `output`.
```
ffmpeg -i <input0> -i <input1> -c copy -map 0:0 -map 1:1 -shortest <output>
```
* [`-c copy`](http://ffmpeg.org/ffmpeg.html#Stream-copy) copy the streams, not re-encoded, so there will be no quality loss.
* [`-map`](http://ffmpeg.org/ffmpeg.html#Advanced-options) designates one or more input streams as a source for the output file. Each input stream is identified by the input file index.
* [`-shortest`](http://ffmpeg.org/ffmpeg-all.html#Main-options) will cause the output duration to match the duration of the shortest input stream.

## Transcoding

List available encoders and decoders.
```
ffmpeg -encoders
ffmpeg -decoders
ffmpeg -formats
```

Decode input.
```
ffmpeg -c:a <codec> -c:v <codec> -i <input> <output>
```

Encode output.
```
ffmpeg -i <input> -c:a <codec> -c:v <codec> <output>
```

### x264

This section focuses on the [x264](https://trac.ffmpeg.org/wiki/Encode/H.264) transcoder.

Encode a video.
```
ffmpeg -i <input> -preset <preset> -crf <crf> <output>
```
* [`-preset`](https://trac.ffmpeg.org/wiki/Encode/H.264) controls the speed of the compression process.
* [`-crf`](https://trac.ffmpeg.org/wiki/Encode/H.264#crf) or Constant Rate Factor controls the output quality. The lower crf, the higher the quality (range 0-51). The default value is 23, and visually lossless compression corresponds to 18.

Preset.
```
ultrafast
superfast
veryfast
faster
fast
medium – default preset
slow
slower
veryslow
placebo – ignore this as it is not useful
```
You can see a list of current presets with `-preset help`. If you have the x264 binary installed, you can also see the exact settings these presets apply by running `x264 --fullhelp`.

### NVENC/NVDEC

This section focuses on the [NVIDIA transcoding](https://developer.nvidia.com/blog/nvidia-ffmpeg-transcoding-guide/).

Encode a video.
```
ffmpeg -vsync 0 -hwaccel cuvid -hwaccel_device 0 -c:v h264_cuvid -i <input> -c:a copy -c:v h264_nvenc -b:v 5M <output>
```
* `-vsync 0` prevents duplication or dropping of frames.
* `-hwaccel cuvid` keeps the decoded frames in GPU memory.
* `-hwaccel_device 0` sets the active GPU for decoding and encoding, the work will be executed on the gpu with index 0.
* `-c:v h264_cuvid` selects the NVIDIA hardware accelerated H264 decoder.
* `-c:v h264_nvenc` selects the NVIDIA hardware accelerated H264 encoder.
* `-b:v 5M` sets the output bitrate to 5Mb/s.

## Editing

### Trim

```
ffmpeg -ss <start> -t <duration> -i <input> -c copy <output>
```
* [`-ss`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the start time, e.g. `00:01:23.000` or `83` (in seconds).
* [`-t`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the duration of the clip.
* [`-to`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the end time, `-to` and `-t` are mutually exclusive and `-t` has priority.
* [`-c`](http://ffmpeg.org/ffmpeg-all.html#Main-options) copy copies the first video, audio, and subtitle bitstream from the input to the output file without re-encoding them. This won't harm the quality and make the command run within seconds.

### Loop

Loop a video `n` times.
```
ffmpeg -stream_loop <n> -i <input> -c copy <output>
```
* Loop `0` means no loop, loop `-1` means infinite loop. 

### Speed Up/Slow Down

This section describes [how to change the speed of a stream](https://trac.ffmpeg.org/wiki/How%20to%20speed%20up%20/%20slow%20down%20a%20video).

Change the speed of a video stream using the [setpts](http://ffmpeg.org/ffmpeg-all.html#setpts_002c-asetpts) video filter (requires re-encoding).
```
ffmpeg -i <input> -vf "setpts=1.0*PTS" <output>
```
* The filter works by changing the presentation timestamp (PTS) of each video frame.
* To speed up use a multiplier lower than 1.
* To slow down use a multiplier higher than 1.

Change the speed of an audio stream using the [atempo](http://ffmpeg.org/ffmpeg-all.html#atempo) audio filter.
```
ffmpeg -i <input> -af "atempo=1.0" <output>
```
* The `atempo` filter is limited to using values between 0.5 and 2.0.
* To speed up use a multiplier lower than 1.
* To slow down use a multiplier higher than 1.

### Delay

Delay audio.
```
ffmpeg -i <input> -itsoffset <time> -i <input> -map 0:v -map 1:a -c:v copy -c:a copy <output>
```
* [`-itsoffset`](https://ffmpeg.org/ffmpeg.html#Main-options) specifies the time to delay.

Delay video.
```
ffmpeg -i <input> -itsoffset <time> -i <input> -map 1:v -map 0:a -c:v copy -c:a copy <output>
```
* [`-itsoffset`](https://ffmpeg.org/ffmpeg.html#Main-options) specifies the time to delay, e.g. `3.00` seconds.

### Volume

Increase audio volume.
```
ffmpeg -i <input> -af "volume=1.5" -c:v copy <output>
ffmpeg -i <input> -af "volume=10dB" -c:v copy <output>
```

Mute audio in an interval.
```
ffmpeg -i <input> -af "volume=enable='between(t,5,10)':volume=0" -c:v copy <output>
```

### Rotate

Rotate 90 degrees clockwise.
```
ffmpeg -i <input> -vf "transpose=1" <output>
```

Rotate 180 degrees clockwise.
```
ffmpeg -i <input> -vf "transpose=2,transpose=2" <output>
```

Transpose.
```
0 = 90 CounterCLockwise and Vertical Flip (default)
1 = 90 Clockwise
2 = 90 CounterClockwise
3 = 90 Clockwise and Vertical Flip
```

### Scale

Resize a video.
```
ffmpeg -i <input> -s <resoluton> -c:a copy <output>
```
* [`-s`](https://ffmpeg.org/ffmpeg.html#Video-Options) sets the frame size.

Scale a video.
```
ffmpeg -i <input> -c:a copy -vf scale=720:-1 <output>
```
* [`scale`](https://ffmpeg.org/ffmpeg.html#Video-Options) filter scales the video to the specified resolution.
 * `-1` sets the correct width or height to keep the aspect ratio.
 * `-2` scales as close to the aspect ratio but rounds to an even number.

Some codecs, like `libx264` requires even values, odd values result in the error `width or height not divisible by 2`. To scale with a given width or height value use `scale="1280:trunc(ow/a/2)*2"` or `scale="trunc(oh*a/2)*2:720"`.

### Slice

Extract all the input frames.
```
ffmpeg -i <input> out%d.png
```

Extract a specified number of frames per second.
```
ffmpeg -i <input> -r <fps> out%d.png
```
* [`-r`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies the number of frames per second.

Extract frames at a specific time.
```
ffmpeg -i <input> -ss <time> -vframes <frames> out%d.png
```
* [`-ss`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the time, e.g. `00:00:10.000` or `10` (in seconds).
* [`-vframes`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies the number of frames.

Create a video slideshow from images.
```
ffmpeg -r <ips> -i img%03d.png -c:v libx264 -vframes <fps> -pix_fmt <format> <output>
```
* [`-r`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies the image frame rate.
* [`-vframes`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies the frame rate of the output.
* [`-pix_fmt`](https://ffmpeg.org/ffmpeg.html#Advanced-Video-options) specifies the pixel format, e.g. `yuv420p`.

### GIF

This section describes [how to create a high quality GIF](http://blog.pkh.me/p/21-high-quality-gif-with-ffmpeg.html).

Create a GIF using color palettes.
```
ffmpeg -i <input> -filter_complex "[0:v] palettegen" palette.png
ffmpeg -i <input> -i palette.png -filter_complex "[0:v][1:v] paletteuse" out.gif

ffmpeg -i <input> -vf "split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" out.gif

ffmpeg -i <input> -vf "split[s0][s1];[s0]palettegen=stats_mode=single[p];[s1][p]paletteuse=new=1" out.gif
```
* [`palettegen`](https://ffmpeg.org/ffmpeg-filters.html#palettegen) generates a color palette, `palettegen=stats_mode=single` generates a new palette for every input frame.
* [`paletteuse`](https://ffmpeg.org/ffmpeg-filters.html#paletteuse) uses a color palette, `paletteuse=new=1` uses a new palette for each frame.

### Draw

This section has examples of the video filter [drawtext](https://ffmpeg.org/ffmpeg-filters.html#drawtext).

Draw frame number and timestamp.
```
ffplay -i <input> -vf "drawtext=text='frame %{frame_num}%{pts\:hms}': x=(w-tw)/2: y=h-(2*lh): fontcolor=white: fontsize=20: box=1: boxcolor=black: boxborderw=5"
```
* On Windows, escape the sequences of form `%{...}` with `%`.

### Metadata

Remove metadata.
```
ffmpeg -i <input> -map_metadata -1 <output>
```

## Streaming

### RTP

Play a stream.
```
ffmpeg -protocol_whitelist file,udp,rtp -i <sdp> <output>
ffplay -i <sdp> -protocol_whitelist file,udp,rtp

ffmpeg -protocol_whitelist rtp,udp -i "rtp://<ip>:<port>" <output>
ffplay -protocol_whitelist rtp,udp -i "rtp://<ip>:<port>"
```

Serve a stream.
```
ffmpeg -re -thread_queue_size 4 -i <input> -strict 2 -acodec copy -vn -f rtp rtp://<ip>:<audio_port> -vcodec copy -an -f rtp rtp://<ip>:<video_port> -sdp_file <sdp>
```

Serve an RTP MPEG-TS stream.
```
ffmpeg -re -i <input> -c:v copy -c:a copy -f rtp_mpegts -sdp_file <sdp> "rtp://<ip>:<port>"
```

### RTSP

Play a stream.
```
ffplay -i rtsp://@<ip>:<port>/<path/to/stream>.<sdp|mp4|mov|avi|etc>
```

Record to file.
```
ffmpeg -i rtsp://@<ip>:<port>/<path/to/stream>.<sdp|mp4|mov|avi|etc> -acodec copy -vcodec copy <output>
```

### RTMP

Publish a stream.
```
ffmpeg -re -i <input> -acodec copy -vcodec copy -f <flv|webm|etc> rtmp://<ip>:1935/<application>/<stream_name>/<stream_key>
```

Play a stream.
```
ffplay -i rtmp://<ip>:1935/<application>/<stream_name>
ffplay -i "rtmp://<ip>:1935/<application>/<stream_name> live=1"
```

### HLS

Play a stream.
```
ffplay -i http://<ip>:<port>/<application>/<stream_name>.m3u8
```

Download a stream.
```
ffmpeg -protocol_whitelist file,http,https,tcp,tls -i http://<ip>:<port>/<application>/<stream_name>.m3u8 -c copy -bsf:a aac_adtstoasc <output>
```

Convert an input to `.m3u8` list and `.ts` packets.
```
ffmpeg -i <input> -codec: copy -start_number 0 -hls_time 10 -hls_list_size 0 -f hls output.m3u8
```

### DASH

Play a stream.
```
ffplay -i http://<ip>:<port>/<application>/<stream_name>.mpd
```

### SRT

🚩 **FFmpeg needs to be compiled with `--enable-libsrt`.**

Listen for connections to send a stream.
```
ffmpeg -i <input> srt://:9710?mode=listener
ffmpeg -i <input> srt://:9710?mode=listener&latency=500
```

Play a stream.
```
ffplay -i srt://192.168.1.1:9710?mode=caller
```

Receive a stream.
```
ffmpeg -i srt://192.168.1.1:9710?mode=caller <output>
```

### NDI

🚩 **NDI removed from FFmpeg due to a [license violation](https://trac.ffmpeg.org/ticket/7589).**

List the available NDI sources.
```
ffmpeg -f libndi_newtek -find_sources 1 -i dummy
```

Play a NDI stream.
```
ffplay -f libndi_newtek -i "NDI Input Stream"
```

Stream an input to a NDI stream.
```
ffmpeg -re -i <input> -f libndi_newtek -pix_fmt uyvy422 "NDI Output Stream"
```

Stream a NDI stream to an output.
```
ffmpeg -f libndi_newtek -i "NDI Input Stream" <output>
```

### Synchronization

Synchronize audio and video.
```
ffmpeg -vsync drop -fflags +discardcorrupt -i <input> <output>
ffplay -sync ext -fflags +discardcorrupt -framedrop -i <input>
```
* `-sync ext` sets the master clock to an external source to play in realtime. The master clock is used to control audio-video synchronization. Values are `audio`, `video` and `ext`, default is `audio`.
* `-fflags +discardcorrupt` discards corrupt packets.
* `-framedrop` drops video frames if video is out of sync. Enabled by default if the master clock is not set to video. Use this option to enable frame dropping for all master clock sources.

Video sync method `vsync`.
* `passthrough (0)` Each frame is passed with its timestamp from the demuxer to the muxer.
* `cfr (1)` Frames will be duplicated and dropped to achieve exactly the requested constant frame rate.
* `vfr (2)` Frames are passed through with their timestamp or dropped so as to prevent 2 frames from having the same timestamp.
* `drop` As passthrough but destroys all timestamps, making the muxer generate fresh timestamps based on frame-rate.
* `auto (-1)` Chooses between cfr and vfr depending on muxer capabilities. This is the default method.

### Latency

Minimize live stream latency.
```
ffmpeg -fflags nobuffer -flags low_delay -reorder_queue_size 0 -i <input> <output>
ffplay -i <input> -fflags nobuffer -flags low_delay -reorder_queue_size 0
```
* `-fflags nobuffer` reduces the latency introduced by optional buffering.
* `-flags low_delay` forces low delay.
* `-reorder_queue_size 0` sets the number of packets to buffer for handling of reordered packets to 0.

## Devices

This section describes the input and output devices provided by the [libavdevice](https://ffmpeg.org/ffmpeg-devices.html) library.

### DirectShow

Windows [DirectShow](https://trac.ffmpeg.org/wiki/DirectShow) input devices.

List devices.
```
ffmpeg -list_devices true -f dshow -i dummy
```

List options.
```
ffmpeg -list_options true -f dshow -i audio="Microphone"
ffmpeg -list_options true -f dshow -i video="Camera"
```

Play camera.
```
ffplay -f dshow -i audio="Microphone":video="Camera"
```

Record to file.
```
ffmpeg -f dshow -i audio="Microphone":video="Camera" <output>
ffmpeg -f dshow -video_size <resolution> -framerate <fps> -pixel_format <pixel_format> -i video="Camera" <output>
ffmpeg -f dshow -video_size 1280x720 -framerate 30 -pixel_format yuyv422 -i video="Camera" output.mp4
```

## Options

| Option | Description |
| - | - |
| [-an](https://ffmpeg.org/ffmpeg.html#Audio-Options) | Blocks all audio streams from being filtered or being automatically selected or mapped for any output. |
| [-vn](https://ffmpeg.org/ffmpeg.html#Video-Options) | Blocks all video streams from being filtered or being automatically selected or mapped for any output. |
| [-sn](https://ffmpeg.org/ffmpeg.html#Subtitle-options) | Blocks all subtitle streams from being filtered or being automatically selected or mapped for any output. |
| [-codec:a](https://ffmpeg.org/ffmpeg.html#Main-options)<br>[-c:a](https://ffmpeg.org/ffmpeg.html#Main-options)<br>[-acodec](https://ffmpeg.org/ffmpeg.html#Main-options) | Select the encoder or decoder for the audio stream. |
| [-codec:v](https://ffmpeg.org/ffmpeg.html#Main-options)<br>[-c:v](https://ffmpeg.org/ffmpeg.html#Main-options)<br>[-vcodec](https://ffmpeg.org/ffmpeg.html#Main-options) | Select the encoder or decoder for the video stream. |
| [-filter:a](https://ffmpeg.org/ffmpeg.html#Main-options)<br>[-af](https://ffmpeg.org/ffmpeg.html#Audio-Options) | Create an audio filtergraph. |
| [-filter:v](https://ffmpeg.org/ffmpeg.html#Main-options)<br>[-vf](https://ffmpeg.org/ffmpeg.html#Video-Options) | Create a video filtergraph. |
| [-r](https://ffmpeg.org/ffmpeg.html#Video-Options) | Sets the frame rate. |
| [-re](https://ffmpeg.org/ffmpeg.html#Advanced-options) | Reads input at native frame rate. By default ffmpeg attempts to read the input as fast as possible. |
| [-f](https://ffmpeg.org/ffmpeg.html#Main-options) | Forces input or output file format. The format is normally auto detected for input files and guessed from the file extension for output files, so this option is not needed in most cases. |
