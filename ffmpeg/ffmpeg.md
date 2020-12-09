# FFmpeg

<p align="center"><img align="center" src="ffmpeg.png"></p>

[FFmpeg](https://www.ffmpeg.org/) is a complete, cross-platform solution to record, convert and stream audio and video.

```
ffmpeg -version
```

## Convert audio and video
```
ffmpeg -i input.mp4 output.avi
```

## Mux

Copy the video from `input0.mp4` and audio from `input1.mp4`.
```
ffmpeg -i input0.mp4 -i input1.mp4 -c copy -map 0:0 -map 1:1 -shortest output.mp4
```
* [`-c copy`](http://ffmpeg.org/ffmpeg.html#Stream-copy) copy the streams, not re-encoded, so there will be no quality loss.
* [`-shortest`](http://ffmpeg.org/ffmpeg-all.html#Main-options) will cause the output duration to match the duration of the shortest input stream.
* [`-map`](http://ffmpeg.org/ffmpeg.html#Advanced-options) designates one or more input streams as a source for the output file. Each input stream is identified by the input file index.

## Remux

Remux a mkv into mp4.
```
ffmpeg -i input.mkv -c:v copy -c:a copy output.mp4
```

## Transcoding

List available encoders and decoders.
```
ffmpeg -encoders
ffmpeg -decoders
```

Decode input.
```
ffmpeg -c:a <codec> -c:v <codec> -i <input> <output>
```

Encode output.
```
ffmpeg -i <input> -c:a <codec> -c:v <codec> <output>
```

### Encoding H264 [:link:](https://trac.ffmpeg.org/wiki/Encode/H.264)
```
ffmpeg -i input.mp4 -preset <preset> -crf <crf> output.mp4
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

### NVENC/NVDEC [:link:](https://developer.nvidia.com/blog/nvidia-ffmpeg-transcoding-guide/)
```
ffmpeg -vsync 0 -hwaccel cuvid -hwaccel_device 0 -c:v h264_cuvid -i input.mp4 -c:a copy -c:v h264_nvenc -b:v 5M output.mp4
```
* `-vsync 0` prevents duplication or dropping of frames.
* `-hwaccel cuvid` keeps the decoded frames in GPU memory.
* `-hwaccel_device 0` sets the active GPU for decoding and encoding, the work will be executed on the gpu with index 0.
* `-c:v h264_cuvid` selects the NVIDIA hardware accelerated H264 decoder.
* `-c:v h264_nvenc` selects the NVIDIA hardware accelerated H264 encoder.
* `-b:v 5M` sets the output bitrate to 5Mb/s.

## Editing

### Trimming

```
ffmpeg -ss <start> -i input.mp4 -t <duration> -c copy output.mp4
```
* [`-ss`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the start time, e.g. `00:01:23.000` or `83` (in seconds).
* [`-t`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the duration of the clip (same format).
* [`-to`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the end time, `-to` and `-t` are mutually exclusive and `-t` has priority.
* [`-c`](http://ffmpeg.org/ffmpeg-all.html#Main-options) copy copies the first video, audio, and subtitle bitstream from the input to the output file without re-encoding them. This won't harm the quality and make the command run within seconds.

### Rotating

Rotate 90 degrees clockwise.
```
ffmpeg -i input.mov -vf "transpose=1" output.mov
```

Rotate 180 degrees clockwise.
```
ffmpeg -i input.mov -vf "transpose=2,transpose=2" output.mov
```

Transpose.
```
0 = 90 CounterCLockwise and Vertical Flip (default)
1 = 90 Clockwise
2 = 90 CounterClockwise
3 = 90 Clockwise and Vertical Flip
```

### Slicing

Extract all the input frames.
```
ffmpeg -i <input> out%d.png
```

Extract a specified number of frames per second.
```
ffmpeg -i <input> -r <fps> out%d.png
```
* [`-r`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies the
number of frames per second.

Extract frames at a specific time.
```
ffmpeg -i <input> -ss <time> -vframes <frames> thumb.png
```
* [`-ss`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the
time, e.g. `00:00:10.000` or `10` (in seconds).
* [`-vframes`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies
the number of frames.

Create a video slideshow from images.
```
ffmpeg -r <ips> -i img%03d.png -c:v libx264 -vframes <fps> -pix_fmt <format> <output>
```
* [`-r`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies the
image frame rate.
* [`-vframes`](https://ffmpeg.org/ffmpeg.html#Video-Options) specifies
the frame rate of the output.
* [`-pix_fmt`](https://ffmpeg.org/ffmpeg.html#Advanced-Video-options)
specifies the pixel format, e.g. `yuv420p`.

## RTP

[Real-time Transport Protocol (RTP)](https://en.wikipedia.org/wiki/Real-time_Transport_Protocol) is a network protocol used in communication and entertainment systems that involve streaming media.
```
ffmpeg -protocol_whitelist file,udp,rtp -i <sdp> <output>
ffplay -i <sdp> -protocol_whitelist file,udp,rtp
```

## HLS

[HTTP Live Streaming(HLS)](https://en.wikipedia.org/wiki/HTTP_Live_Streaming) is an HTTP-based adaptive bitrate streaming communications protocol.

Download and concatenate the video fragments.
```
ffmpeg -protocol_whitelist file,http,https,tcp,tls -i <m3u8> -c copy
-bsf:a aac_adtstoasc <output>
```

## Latency

Minimize live stream latency.
```
ffplay -i <input> -fflags nobuffer -flags low_delay -reorder_queue_size 0
```
* `-fflags nobuffer` reduces the latency introduced by optional buffering.
* `-flags low_delay` forces low delay.
* `-reorder_queue_size` sets the number of packets to buffer for handling of reordered packets to 0.
* `-framedrop` drops video frames if video is out of sync. Enabled by default if the master clock is not set to video. Use this option to enable frame dropping for all master clock sources.

## Options

| Option | Description |
| - | - |
| [-an](https://ffmpeg.org/ffmpeg.html#Audio-Options) | Blocks all audio streams from being filtered or being automatically selected or mapped for any output. |
| [-vn](https://ffmpeg.org/ffmpeg.html#Video-Options) | Blocks all video streams from being filtered or being automatically selected or mapped for any output. |
| [-sn](https://ffmpeg.org/ffmpeg.html#Subtitle-options) | Blocks all subtitle streams from being filtered or being automatically selected or mapped for any output. |
| [-r](https://ffmpeg.org/ffmpeg.html#Video-Options) | Sets the frame rate. |
| [-re](https://ffmpeg.org/ffmpeg.html#Advanced-options) | Reads input at native frame rate. By default ffmpeg attempts to read the input as fast as possible. |
| [-f](https://ffmpeg.org/ffmpeg.html#Main-options) | Forces input or output file format. The format is normally auto detected for input files and guessed from the file extension for output files, so this option is not needed in most cases. |
| [-stream_loop](http://ffmpeg.org/ffmpeg-all.html#Main-options) | Sets the number of times input stream shall be looped. Loop 0 means no loop, loop -1 means infinite loop. |
