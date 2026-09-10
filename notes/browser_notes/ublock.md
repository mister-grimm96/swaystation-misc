# custom ublock links

## custom ublock links

```
! Hide recommended videos after watching a video
www.youtube.com##ytd-watch-next-secondary-results-renderer

! Hide “Up next” sidebar
www.youtube.com##ytd-compact-video-renderer

! Hide “Recommended” carousels
www.youtube.com##ytd-browse[page-subtype="home"] ytd-rich-shelf-renderer

! Hide Shorts suggestions
www.youtube.com##ytd-reel-shelf-renderer

! Block RoelVandePaar everywhere
youtube.com##ytd-rich-item-renderer:has(a[href^="/@RoelVandePaar"])
youtube.com##ytd-video-renderer:has(a[href^="/@RoelVandePaar"])
youtube.com##ytd-compact-video-renderer:has(a[href^="/@RoelVandePaar"])
```

full-link : https://www.reddit.com/r/uBlockOrigin/wiki/solutions/youtube/#wiki_suggested_videos
