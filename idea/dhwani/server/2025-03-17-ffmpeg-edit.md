ffmpeg -i output.mkv -c:v copy -c:a copy output.mp4

# Editing an MKV Video with FFmpeg

This guide explains how to use FFmpeg to remove specific segments from an MKV video based on timestamps (0:00-0:45, 1:08-1:53, and 2:15-3:11) and keep the remaining parts.

## Assumptions
- Input file: `input.mkv`
- Sections to keep: 0:45-1:08, 1:53-2:15, and 3:11 to the end
- Video duration exceeds 3:11

## Method 1: Cut and Concatenate (No Re-encoding)
This method uses stream copying for speed and concatenates the retained segments.

### Step 1: Extract Segments
Run the following commands to split the video:

```bash
# Segment 1: 0:00 to 0:48
ffmpeg -i input.mkv -ss 00:00:00 -to 00:00:48 -c:v copy -c:a copy part1.mkv

# Segment 2: 1:30 to 1:53
ffmpeg -i input.mkv -ss 00:01:30 -to 00:01:53 -c:v copy -c:a copy part2.mkv

# Segment 3: 2.15 to 3:11 
ffmpeg -i input.mkv -ss 00:02:15 -to 00:03:11 -c:v copy -c:a copy part3.mkv
```


- Step 2

Create file - list.txt
```bash
file 'part1.mkv'
file 'part2.mkv'
file 'part3.mkv'
```

- Step 3: Concatenate
Combine the segments into a single file:


```bash
ffmpeg -f concat -safe 0 -i list.txt -c copy output.mkv
```


- Convert to mp4

```bash
ffmpeg -i output.mkv -c:v copy -c:a copy output.mp4
```


-EDit the video for Android APP

ffmpeg -i output.mp4 -filter:v "crop=640:1000:0:0" release-video.mp4