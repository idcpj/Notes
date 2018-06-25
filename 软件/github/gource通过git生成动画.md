[TOC]

> [github](https://github.com/acaudwell/Gource)


## 安装 
1. mac
`brew install gource`

## 使用
 直接在有 项目中
 `gource` 即可
 
 ## 生成视频
 `gource -1280x720 -o - | ffmpeg -y -r 60 -f image2pipe -vcodec ppm -i - -vcodec libx264 -preset ultrafast -pix_fmt yuv420p -crf 1 -threads 0 -bf 0 gource.mp4
`