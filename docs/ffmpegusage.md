# Common ffmpeg usage

- Convert an encoded video file to another encode type video file, e.g
```
Ffmpeg -i in.h264 out.yuv
```

- Rescale, skip frames, strip Y channel:
```
ffmpeg -i input.mp4 -vf scale=512:512 -r 5 -pix_fmt gray Out.yuv
```

- Crop video:
```
ffmpeg -i tmp.mp4 -pix_fmt gray -filter:v crop=416:416:80:80 out2_croped.yuv
```
