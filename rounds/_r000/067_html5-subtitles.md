---
layout: post
title: HTML5 subtitles
date: 2020-07-03 11:55:03 -0700
#date_updated:  # Optional and formatted like 'date' above
description: Example of using `track` and `video` HTML5 elements
time_to_live: 1800
---



Example of using `track` and `video` HTML5 elements...


```html
<video preload="metadata" controls>
  <source src="videos/name.mp4" type="video/mp4">
  <track src="en.vtt" srclang="en" label="English" kind="subtitles" default>
  <track src="es.vtt" srclang="es" label="Español" kind="subtitles">
</video>
```


## Attribution
[heading__attribution]: #attribution


[MDN -- Adding captions and subtitles to HTML5 video](https://developer.mozilla.org/en-US/docs/Web/Guide/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video)
