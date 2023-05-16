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

- Transfer file to nginx rtmp/hls server
```
//output stream with encoder copy from the input source
ffmpeg -re -i bbb_sunflower_1080p_30fps_normal.mp4 -vcodec copy -loop -1 -c:a aac -b:a 160k -ar 44100 -strict -2 -f flv rtmp:192.168.72.20/live/bbb

//output stream with another encoder, here it's h264
ffmpeg -re -i bbb_sunflower_1080p_30fps_normal.mp4  -vf scale=-1:270 -vcodec libx264  -f flv rtmp:192.168.72.20/live/bbb
```
