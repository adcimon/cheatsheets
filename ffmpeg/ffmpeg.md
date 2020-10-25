# FFmpeg

<p align="center"><img align="center" src="ffmpeg.png"></p>

[FFmpeg](https://www.ffmpeg.org/) is a complete, cross-platform solution to record, convert and stream audio and video.

Convert audio and video.
```
ffmpeg -i <input.mp4> <output.avi>
```

## Remux

Remux a mkv into mp4.
```
ffmpeg -i <input.mkv> -c:v copy -c:a copy <output.mp4>
```

## Encoding

Encoding H264 (https://trac.ffmpeg.org/wiki/Encode/H.264)
```
ffmpeg -i <input.mp4> -preset slower -crf 18 <output.mp4>
```
* [`-preset`](https://trac.ffmpeg.org/wiki/Encode/H.264) controls the speed of the compression process.
* [`-crf`](https://trac.ffmpeg.org/wiki/Encode/H.264#crf) or Constant Rate Factor controls the output quality. The lower crf, the higher the quality (range 0-51). The default value is 23, and visually lossless compression corresponds to 18.

## Trimming

```
ffmpeg -ss <start> -i <input.mp4> -t <duration> -c copy <output.mp4>
```
* [`-ss`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the start time, e.g. `00:01:23.000` or `83` (in seconds).
* [`-t`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the duration of the clip (same format).
* [`-to`](http://ffmpeg.org/ffmpeg-all.html#Main-options) specifies the end time, `-to` and `-t` are mutually exclusive and `-t` has priority.
* [`-c`](http://ffmpeg.org/ffmpeg-all.html#Main-options) copy copies the first video, audio, and subtitle bitstream from the input to the output file without re-encoding them. This won't harm the quality and make the command run within seconds.

## Rotate

Rotate 90 degrees clockwise.
```
ffmpeg -i <input.mov> -vf "transpose=1" <output.mov>
```

Rotate 180 degrees clockwise.
```
ffmpeg -i <input.mov> -vf "transpose=2,transpose=2" <output.mov>
```

Transpose.
```
0 = 90 CounterCLockwise and Vertical Flip (default)
1 = 90 Clockwise
2 = 90 CounterClockwise
3 = 90 Clockwise and Vertical Flip
```

## Audio

| Audio options | |
| - | - |
| -an | Disable audio. |

## Video

| Video options | |
| - | - |
| -r | Frame rate. |