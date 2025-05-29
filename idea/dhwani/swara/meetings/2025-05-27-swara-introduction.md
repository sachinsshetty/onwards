Swara - Introduction - 27 May, 2025

- Resources/ GPU server requirements
  - Experiments / Inference
    - 1x H100 GPU : 2.49 $/hour
      - 2.49 * 24 : 59.76 $/day 
      - 1852.56 $ /month
      - 22,230.72 $/year
  - Training 
    - 10 X H100
      - 18525.6 $/month

- Phase 1 : Text to Song
  - Use compositions/ varna's from purundaradasa.org and create simple songs without music

- Phase 2 : Song + Music
  - Sync music to songs with Audiocraft

- Phase 3 : Editable songs
  - Generate Music based on user requests in real-time



- Phase 1  - Detail
  - Data collection - https://tkgovindarao.org/compositions.php
  - Data transformation
    - parse document with LLM to convert to Huggingface/dataset format
  - Literature survey and experiments
    - Text to Song models
    - Availability of Open source / Indian language models
  - Annotation and feedback loop software
    - System design, development and deploymeny
  - Inference server setup
    - llama.cpp server optimsation > CPU/GPU compatbility
  - tool_call with qwen3 for music embedings
  - IndicSeamless - Audio conversion to other languages