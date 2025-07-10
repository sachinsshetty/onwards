Google AI Future Fund

dwani.ai now has Multi-modal Inference API capability. 
Along with the Android App, we provide self-hosting options using Open Weight models. 

1. Funding 
    - Yes, I am looking for seed grants upto USD 100k for developer salary and organisation expenses for 1 year. dwani.ai is bootstrapped and I have been working full-time since February 2025.
    - We require GPU's for dwani.ai inference - we are constrained by GPU availability. 

2. Traction 
    - Android App has 300 total installs, with 100+ active installs. 
    - We have conducted 3 workshops for students. Total 500 students were provided an introduction to get started building AI applications for Indian languages.  https://dwani.ai/dwani-ai-workshop.pdf .
    - We conduct one workshop per month at Universities. We do not charge the students/university , Entry is open to all.  For July we have 2 workshops planned.
    
3. AI Models and Technology
    - https://github.com/dwani-ai/deploy  - contains the detailed steps for self-hosting dwani.ai. 
    - We are using Nvidia GH200/ arm64 on lambda.ai to host one instance of dwani.ai  
    - Models 
        - Text + Vision : google/gemma-12B-IT, 
        - Text to Speech ; ai4bharat/IndicF5, onnx-community/Kokora-82M-v1.0-ONNX 
        - Speech Transcription - ai4bharat/indic-conformer-600m-mulitlingual, Systran/faster-whisper-larger-v3
        - Tool Call : qwen/qwen3-32B
    - What is working :
        - ASR/Speech transcription is great with AI4Bharat models for Indian languages. 
        - Text to Speech : IndicF5 is good for Indian languages, but it is compute intensive. 
        - Gemma3 works well for Text and Vision inference for English. Kannada and German.
    - What is on your wishlist ?
        - We would like tool_call to be improved in the next release of Gemma,
        - I am yet to explore in depth Gemma-3n with Matroshka Transformers for Multi-modal inputs. It had a few issues on release day .