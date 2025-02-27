Cloud provider benchmarks

- Setup done on Huggingface Spaces 


    - ASR - Automatic Speech Recognition


### How to Use the Service

1. With curl

You can test the service using `curl` commands. Below are examples for both service modes:

#### High Latency Service - CPU server

```sh curl_high_latency.sh
curl -X 'POST' \
  'https://gaganyatri-asr-indic-server-cpu.hf.space/transcribe/?language=kannada' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@samples/kannada_sample_2.wav;type=audio/x-wav'
```

#### Low Latency Service - GPU service on Demand

```sh curl_low_latency.sh
curl -X 'POST' \
  'https://gaganyatri-asr-indic-server.hf.space/transcribe/?language=kannada' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@samples/kannada_sample_2.wav;type=audio/x-wav'
```

2. Via Swagger UI 

- **URL**: [High Latency ASR Service](https://huggingface.co/spaces/gaganyatri/asr_indic_server_cpu)

- **URL**: [Low Latency ASR Service](https://huggingface.co/spaces/gaganyatri/asr_indic_server_cpu)


- Text to Speech 


We have hosted a Text to Speech (TTS) service that can be used to verify the accuracy of Speech generation. The service is available in two modes:

## Usage

### How to Use the Service

You can test the service using `curl` commands. Below are examples for both service modes:

#### High Latency Service

```bash kannada_example.sh
curl -X 'POST' \
  'https://gaganyatri-tts-indic-server.hf.space/v1/audio/speech' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{"input": "ಉದ್ಯಾನದಲ್ಲಿ ಮಕ್ಕಳ ಆಟವಾಡುತ್ತಿದ್ದಾರೆ ಮತ್ತು ಪಕ್ಷಿಗಳು ಚಿಲಿಪಿಲಿ ಮಾಡುತ್ತಿವೆ.", "voice": "A female speaker delivers a slightly expressive and animated speech with a moderate speed and pitch. The recording is of very high quality, with the speakers voice sounding clear and very close up."}'  -o audio_kannada_gpu_cloud.mp3
```

#### Low Latency Service

```bash kannada_example.sh
curl -X 'POST' \
  'https://gaganyatri-tts-indic-server-cpu.hf.space/v1/audio/speech' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{"input": "ಉದ್ಯಾನದಲ್ಲಿ ಮಕ್ಕಳ ಆಟವಾಡುತ್ತಿದ್ದಾರೆ ಮತ್ತು ಪಕ್ಷಿಗಳು ಚಿಲಿಪಿಲಿ ಮಾಡುತ್ತಿವೆ.", "voice": "A female speaker delivers a slightly expressive and animated speech with a moderate speed and pitch. The recording is of very high quality, with the speakers voice sounding clear and very close up."}'  -o audio_kannada_cpu_cloud.mp3
```

3. Translation on Huggingface Spaces



4. Test  TTS + ASR for easy verification. 

Test it on terminal/command line /  postman / Insomnia 


1. Use the Text to Speech (TTS) to generate the speech by providing Kannada text. It creates a .wav file with name "audio_kannada_gpu_cloud.wav"
```
curl -X 'POST' \
  'https://gaganyatri-tts-indic-server.hf.space/v1/audio/speech' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{"input": "ಉದ್ಯಾನದಲ್ಲಿ ಮಕ್ಕಳ ಆಟವಾಡುತ್ತಿದ್ದಾರೆ ಮತ್ತು ಪಕ್ಷಿಗಳು ಚಿಲಿಪಿಲಿ ಮಾಡುತ್ತಿವೆ.", "voice": "A female speaker delivers a slightly expressive and animated speech with a moderate speed and pitch. The recording is of very high quality, with the speakers voice sounding clear and very close up.",, "response_type": "wav"}'  -o audio_kannada_gpu_cloud.wav

```

2. Now call the ASR - Automatic Speech Recognition by passing the Generated Speech 
```
curl -X 'POST' \
  'https://gaganyatri-asr-indic-server-cpu.hf.space/transcribe/?language=kannada' \
  -H 'accept: application/json' \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@audio_kannada_gpu_cloud.wav;type=audio/x-wav'
```




- Ola Krutrim CLoud

 - ASR setup on Krutrim Cloud 


Watch a quick demo of our project in action! Click the image below to view the video on YouTube.

[![Watch the video](https://img.youtube.com/vi/F0Mo0zjyysM/0.jpg)](https://youtu.be/F0Mo0zjyysM)

We have hosted an Automatic Speech Recognition (ASR) service that can be used to verify the accuracy of audio transcriptions. The service is available in two modes:

We tested A100-NVLINK-Mini for the project. This setup is straightforward to initiate and deploy for basic inference tasks.

OlaKrutrim is an ideal provider for this task. They charge on an hourly basis with a calculated 15-minute interval, ensuring flexibility and cost-effectiveness. There is no long-term commitment required, making it easy to start and stop as needed.
