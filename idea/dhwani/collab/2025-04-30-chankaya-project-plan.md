Chanakya University Project Plan

1. Valmiki - Voice assistant deployment at Chanakya University

2. Indian Knowledge System - Fine-tune model with Kannada dataset


### Project Valmiki
- Deploy Voice Assistant system on campus
- Student built Hardware based project connected to dwani.ai server self-hosted on GPU server
- H/W system    
    - PC Monitor, RaspberryPi 5 / Arduino , Microphone, Speaker, WiFI/LAN
- S/W system
    - Embedded software running a user termnial/client.
        - to collect voice query
        - send it to dwani.ai server
        - play back the audio response 

### Indian Knowledge System
- Collect dataset from different sources
- Design and develop - data modelling and filtering to Instruction Template (LLM Chat Template)
- Version 1 
    - RAG system - to create vector data and provide accurate information about Kannada literature
- Version 2
    - Finetune model using LORA to deploy model at different locations


- May 15 Status
    - document processing
        - vllm server : Gemma3 4B/12B
        - indic translate server - 10/15GB VRAM for best translation with indian languages
        - docs-indic-server : use vllm-server and indic-translate for Document processing
    - Ex : https://huggingface.co/spaces/dwani/indic-pdf-chat-custom
    - pip install dwani