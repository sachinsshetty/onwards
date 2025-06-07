dwani time

tinyurl.com/dwani-time

Feb 20 - June 7 : 2025
Week - 1 - 17
https://youtube.com/shorts/dg-dAEn1704?feature=share

input.txt
file 'imgA.jpg'
duration 3
file 'imgB.jpg'
duration 3



ffmpeg -f concat -safe 0 -i input.txt -vf scale=1920:1080 -c:v libx264 -r 30 -pix_fmt yuv420p output.mp4
