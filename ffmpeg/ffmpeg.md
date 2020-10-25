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