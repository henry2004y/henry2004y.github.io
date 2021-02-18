---
title: Making Videos from Figures
layout: post
tags: [visual]
date: 2019-10-25
author: Hongyang Zhou
---

I have been went through this several times. In the early stage, I was using Matlab for concatenating figures into videos. 
There are some shortcomings with this method:

1 It requires Matlab license  
2 The simple brute force algorithm generates large video files, and you cannot control the output resolution

Then I tried the [VideoIO](https://github.com/JuliaIO/VideoIO.jl) package in Julia, but unfortunately, currently it lacks the support for
VGBA encoding format.

After some searches on the web, I found a neat solution to these kinds of task: [ffmpeg](https://www.ffmpeg.org/). Personally I installed 
it through Macports, but you can download it directly from the website.

# Issues

Although it seems easy to make videos from figures, it is actually not. You need to have some basic understandings of how figures are saved
and how different video formats are structured. I have encountered two major issues in using **ffmpeg**:

1 _Image size must be a multiple of 2_

  My png files generated from Matplotlib have odd pixel numbers for both width and height.  
  From one of the answers posted on [StackOverFlow](https://stackoverflow.com/questions/20847674/ffmpeg-libx264-height-not-divisible-by-2)
  >As required by x264, the "divisible by 2 for width and height" is needed for YUV 4:2:0 chroma subsampled outputs. 4:2:2 would need
  "divisible by 2 for width", and 4:4:4 does not have these restrictions. However, most non-FFmpeg based players can only properly decode 
  4:2:0, so that is why you often see ffmpeg commands with the -pix_fmt yuv420p option when outputting H.264 video.  

2 _Quicktime cannot play a movie file encoded by *ffmpeg*_

  From [ffmpeg wiki](https://trac.ffmpeg.org/wiki/Encode/H.264#Encodingfordumbplayers):
  >You may need to use `-vf format=yuv420p` (or the alias `-pix_fmt yuv420p`) for your output to work in QuickTime and most other players. 
  These players only support the YUV planar color space with 4:2:0 chroma subsampling for H.264 video. Otherwise, depending on your source,
  ffmpeg may output to a pixel format that may be incompatible with these players.
  
  So, as you can see these two problems are related, but not identical.

# Solutions

1 _Image size must be a multiple of 2_

  There is an option **-2** in specifying the size. For example,
  >-vf scale=1280:-2
  Set width to 1280, and height will automatically be calculated to preserve the aspect ratio, and the height will be divisible by 2  
  >-vf scale=-2:720
  Same as above, but with a declared height instead; leaving width to be dealt with by the filter.
  
2 _movie not playable_
  
  Use `-vf format=yuv420p` or `-pix_fmt yuv420p` in the command line options.
  
Finally, the following command works for me:
```
ffmpeg -r 12 -pattern_type glob -i '*.png' -vcodec libx264 -vf scale=640:-2 -pix_fmt yuv420p pi.mp4
```





