Dhwani Workshop - March 2025

- Dhwani is a self-hosted GenAI platform designed to provide voice mode interaction for Kannada and other Indian languages.
- We want to make AI accessible for native local languages
- Dhwani Project [Website](https://slabstech.com/dhwani/)

---


- Workshop Agenda
  - Deploy Gradio App to HuggingFace Spaces
  - Build and Deploy
    - Kannada Text Translator App
    - Kannada AI Text Chat App
    - Kannada Voice AI App

--- 

- Prerequisites
  - Python 3.10 required + VsCode  [ Installed ]
  - Ubuntu 22.04 
  - Huggingface Account 
  - GitHub Account

--- 

- Good to Have, to start hacking immediately
  - Fork the below repositories and clone your forked repository into your computer
    - [https://github.com/slabstech/llm-indic-server](https://github.com/slabstech/llm-indic-server)
    - [https://github.com/slabstech/indic-translate-server](https://github.com/slabstech/indic-translate-server)
    - [https://github.com/slabstech/asr-indic-server](https://github.com/slabstech/asr-indic-server)
    - [https://github.com/slabstech/tts-indic-server](https://github.com/slabstech/tts-indic-server)


---

  - Download the Huggingface model's
  - **Steps**:
    1. **Create a virtual environment**:
    ```bash
    python -m venv venv
    ```
    2. **Activate the virtual environment**:
    ```bash
    source venv/bin/activate
    ```

    3. **Install dependencies**:
        ```bash
        pip install huggingface_hub
        ```
    4. Download the models 
    - tts - ```huggingface_cli download ai4bharat/indic-parler-tts```
    - asr - ```huggingface-cli download ai4bharat/indicconformer_stt_kn_hybrid_rnnt_large```
    - translate - 
        - indic to english - ```huggingface-cli download ai4bharat/indictrans2-indic-en-dist-200M```
        - english to indic - ```huggingface-cli download ai4bharat/indictrans2-en-indic-dist-200M```
        - indic to indic - ```huggingface-cli download ai4bharat/indictrans2-indic-indic-dist-320M ```
    - llm - ```huggingface-cli download Qwen/Qwen2.5-1.5B-Instruct```


---

- How your projects might look like, You can expand and modify for your use case
    - [Dhwani Voice AI]()
    - [Dhwani Translate App]()
    - [Dhwani - Text Chat AI]()
    - [Dhwani ASR]()


---


- YouTube video related to Dhwani
  - [Dhwani Voice AI](https://www.youtube.com/watch?v=L4DGuYj-kjs)
  - [Dhwani - ASR](https://www.youtube.com/watch?v=F0Mo0zjyysM)
  - [Sanjeevi - English](https://www.youtube.com/watch?v=KHK_jaB4D0g)


---

- Join the [Dhwani Discord group](https://discord.gg/WZMCerEZ2P) for updates and collaboration to build Dhwani