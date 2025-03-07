Dhwani Voice- Mobile App



curl -X 'POST'   'https://gaganyatri-llm-indic-server-cpu.hf.space/v1/audio/speech'   -H 'accept: application/json'   -H 'Content-Type: application/json' -H "X-API-Key: your-actual-key"   -d '{
  "input": "ನಿಮ್ಮ ಇನ್‌ಪುಟ್ ಪಠ್ಯವನ್ನು ಇಲ್ಲಿ ಸೇರಿಸಿ",
  
  "voice": "Female speaks with a high pitch at a normal pace in a clear, close-sounding environment. Her neutral tone is captured with excellent audio quality.",
  "model": "ai4bharat/indic-parler-tts",
  "response_format": "mp3",
  "speed": 1,

}' -o test.mp3


curl -X POST "http://localhost:7860/v1/audio/speech" \
     -H "X-API-Key: your-actual-key" \
     -H "Content-Type: application/json" \
     -d '{"input": "ನಿಮ್ಮ ಇನ್‌ಪುಟ್ ಪಠ್ಯವನ್ನು ಇಲ್ಲಿ ಸೇರಿಸಿ", "voice": "Female speaks with a high pitch at a normal pace in a clear, close-sounding environment. Her neutral tone is captured with excellent audio quality.", "model": "ai4bharat/indic-parler-tts", "response_format": "mp3", "speed": 1.0}' \
     --output speech.mp3


https://gaganyatri-llm-indic-server-cpu.hf.space/v1/audio/speech



curl -X POST "http://localhost:7860/v1/audio/speech" \
     -H "X-API-Key: your-secret-api-key" \
     -H "Content-Type: application/json" \
     -d '{"input": "ನಿಮ್ಮ ಇನ್‌ಪುಟ್ ಪಠ್ಯವನ್ನು ಇಲ್ಲಿ ಸೇರಿಸಿ", "voice": "Female speaks with a high pitch at a normal pace in a clear, close-sounding environment. Her neutral tone is captured with excellent audio quality.", "model": "ai4bharat/indic-parler-tts", "response_format": "mp3", "speed": 1.0}' \
     --output speech.mp3


curl -X POST "https://gaganyatri-llm-indic-server-cpu.hf.space/v1/audio/speech" \
     -H "X-API-Key: your-new-secret-api-key" \
     -H "Content-Type: application/json" \
     -d '{"input": "ನಿಮ್ಮ ಇನ್‌ಪುಟ್ ಪಠ್ಯವನ್ನು ಇಲ್ಲಿ ಸೇರಿಸಿ", "voice": "Female speaks with a high pitch at a normal pace in a clear, close-sounding environment. Her neutral tone is captured with excellent audio quality.", "model": "ai4bharat/indic-parler-tts", "response_format": "mp3", "speed": 1.0}' \
     --output speech.mp3

