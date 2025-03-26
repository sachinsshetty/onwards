Dhwani - 4 week - Experiments - March 2025

Below is brief summary

1. Parler-tts: inference speed improved from 2s /word to .5 s / word. 
- latency report : https://github.com/sachinsshetty/onwards/blob/main/idea%2Fdhwani%2Fserver%2F2025-03-16-tts-latency.md

2. Pull Request on parler-tts github repo to enable fast inference. 
- Current version of transformer not able to utilise speed up provided by pytorch.
- Updated to transformer v.50.0 and fixed deprecated functions
- https://github.com/huggingface/parler-tts/pull/206

3. Conducted workshop at Chanakya University on 20th march. Topic - Getting started with Dhwani. 
- Recording: YouTube - https://youtu.be/f5JkJLQJFGA 

- Slides: https://tinyurl.com/dhwani-workshop 

- Source Code: https://github.com/slabstech/dhwani-workshop

4. Dhwani API server - GPU utilization
- to maximize GPU compute and use spare capacity, created API endpoints and made it available for Workshop Attendees to bootstrap projects .
- https://youtu.be/RLIhG1bt8gw