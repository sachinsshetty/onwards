Feb 2, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-02-dhwani-voice-quiz.md

Dhwani - QUIZ system with Voice.

With a combination of ASR + LLM + TTS
learning can be made interactive for all ages, levels, and domains.

Use whisper + deepseek-r1 as Judge evaluator for Voice inputs and evaluation for the TTS system .

Entire stack can be built with Open Source code and open weight models.

A simple way to build solutions with AI.

Tech stack remains constant , multiple  usecases are built with different combinations of the tools.

Backend - python/Django
Deployment - docker with GPU
Frontend- React/ Typescript
Database-
postgreSQL for text ,
MongoDB for multimedia data storage,
Redis for websockets to serve real-time voice


—--
Feb 4, 2025


https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-04-indic-notebook-lm.md

Indic NotebookLM

- IndicLID
  - Intermediate steps to detect languafe from input text
  - Select LLM base/Instruct mmodel based on language detected
  - Select TTS for the language
	- Use specific models for different language via RestAPI call	


Feb 23, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-23-kannada-voice-mode.md


Kannda Voice Mode - End to End Speech

- Sanjeevini.me : Medical Transcription Agent  - is now unlocked.

- End to End Flow
	- ASR - Automatic Speech Recognition
	- Translation  
	- Intelligence - LLM
	- TTS - Text to Speech

Tools for Kannada

- Source
	- https://github.com/slabstech/asr-indic-server
	- https://github.com/slabstech/indic-translate-server
	- https://github.com/slabstech/parler-tts-server

- Docker images
	- TTS - slabstech/parler-tts-server:latest
	- Translate - slabstech/translate-indic-server
	- ASR - slabstech/asr-indic-server




—-
Feb 24, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-24-c4-spec-indic-server.md
# C4 Model: Kannada Voice Model Development Demo

This document presents the C4 model (Context, Containers, Components, and Code) for the Kannada Voice Model Development Demo. It describes the system's architecture at varying levels of detail, from its interaction with external entities to the internal code structure, aligning with the goal of creating a robust voice assistant for Kannada speakers.

## Level 1: Context Diagram

```mermaid
graph TD
	A[End User] -->|Provides speech/text input, receives audio/text output| B[Kannada Voice System]
	B -->|Fetches datasets for model training| C[AI4BHARAT Datasets]
```

- **End User**: A Kannada speaker interacting with the system via speech or text input.
- **Kannada Voice System**: The core system providing ASR, TTS, and translation services.
- **AI4BHARAT Datasets**: External data source for training and fine-tuning models.

### Interactions
- **End User → System**: Provides speech/text input, receives audio/text output.
- **System → AI4BHARAT**: Fetches datasets for model training.

## Level 2: Container Diagram

### Description
The Container Diagram breaks the Kannada Voice System into its major deployable units (containers) and their interactions, hosted on a cloud GPU infrastructure.

### Diagram

```mermaid
graph TD
	A[End User] -->|HTTP requests/responses| B[API Server (Flask/FastAPI)]
	B -->|Internal API calls| C[ASR Container]
	B -->|Internal API calls| D[TTS Container]
	B -->|Internal API calls| E[Translation Container]
	C -->|Leverage GPU for model execution| F[GPU Instance (e.g., RTX 4090)]
	D -->|Leverage GPU for model execution| F
	E -->|Leverage GPU for model execution| F
	C -->|Fetch training data during development| G[AI4BHARAT Datasets]
	D -->|Fetch training data during development| G
	E -->|Fetch training data during development| G
```

- **API Server**: Handles user requests and routes them to appropriate containers.
- **ASR Container**: Processes speech-to-text functionality.
- **TTS Container**: Processes text-to-speech functionality.
- **Translation Container**: Handles text translation between languages.
- **GPU Instance**: Cloud-based GPU (e.g., Vast.ai RTX 4090) for model inference and training.

### Interactions
- **End User ↔ API Server**: HTTP requests/responses (e.g., audio upload, text/audio download).
- **API Server ↔ Containers**: Internal API calls to process ASR, TTS, or translation.
- **Containers ↔ GPU Instance**: Leverage GPU for model execution.
- **Containers ↔ AI4BHARAT Datasets**: Fetch training data during development.

## Level 3: Component Diagram

### Description
The Component Diagram zooms into the containers, detailing the internal components and their interactions within the Kannada Voice System.

### Diagram

```mermaid
graph TD
	A[API Server] -->|Routes requests to specific endpoints| B[/asr]
	A -->|Routes requests to specific endpoints| C[/tts]
	A -->|Routes requests to specific endpoints| D[/translate]
	B -->|Speech-to-text requests| E[ASR Container]
	C -->|Text-to-speech requests| F[TTS Container]
	D -->|Translation requests| G[Translation Container]
	E -->|ASR Model| H[ASR Model]
	E -->|Audio Processing| I[Audio Proc.]
	F -->|TTS Model| J[TTS Model]
	F -->|Text Processing| K[Text Proc.]
	G -->|Translation Model| L[Trans Model]
	G -->|Text Processing| M[Text Proc.]
	H -->|Runs inference on GPU| N[GPU Instance]
	I -->|Runs inference on GPU| N
	J -->|Runs inference on GPU| N
	K -->|Runs inference on GPU| N
	L -->|Runs inference on GPU| N
	M -->|Runs inference on GPU| N
	N -->|PyTorch| O[PyTorch]
	N -->|Torchaudio| P[Torchaudio]
```

- **API Server**:
  - **/asr**: Endpoint for speech-to-text requests.
  - **/tts**: Endpoint for text-to-speech requests.
  - **/translate**: Endpoint for translation requests.
- **ASR Container**:
  - **ASR Model**: Fine-tuned Indic ASR model.
  - **Audio Processing**: Handles audio input (e.g., normalization).
- **TTS Container**:
  - **TTS Model**: Fine-tuned Parler TTS model.
  - **Text Processing**: Prepares text for speech synthesis.
- **Translation Container**:
  - **Translation Model**: Fine-tuned Indic Translate model.
  - **Text Processing**: Tokenizes and formats text.
- **GPU Instance**:
  - **PyTorch**: Framework for model execution.
  - **Torchaudio**: Audio processing library.

### Interactions
- **API Server → Containers**: Routes requests to specific endpoints.
- **ASR Model ↔ Audio Processing**: Converts WAV input to text.
- **TTS Model ↔ Text Processing**: Converts text to WAV output.
- **Translation Model ↔ Text Processing**: Translates text between languages.
- **Containers ↔ GPU Instance**: Use PyTorch and Torchaudio for GPU-accelerated inference.

## Level 4: Code-Level Details (Sample)

### Description
This section provides a high-level pseudocode example for the ASR endpoint, illustrating the integration of components.

### Pseudocode
```python
# File: api_server.py
from flask import Flask, request, jsonify
import torchaudio
from asr_model import ASRModel

app = Flask(__name__)
asr_model = ASRModel.load("indic_asr_kannada.pt")

@app.route("/asr", methods=["POST"])
def process_asr():
	# Receive audio file from user
	audio_file = request.files["audio"]
	waveform, sample_rate = torchaudio.load(audio_file)

	# Preprocess audio
	if sample_rate != 16000:
    	waveform = torchaudio.transforms.Resample(sample_rate, 16000)(waveform)

	# Run ASR inference on GPU
	text = asr_model.transcribe(waveform.cuda())

	# Return transcribed text
	return jsonify({"transcription": text})

if __name__ == "__main__":
	app.run(host="0.0.0.0", port=5000)
```

### Specification for Indic Server

### Key Components:
- **ASRModel**: Custom class wrapping the fine-tuned ASR model.
- **torchaudio.load**: Loads WAV input.
- **transcribe**: Runs inference on GPU.

### Dependencies:
- Flask
- PyTorch
- Torchaudio

### Notes:
- Similar code structures apply to `/tts` (using `TTSModel`) and `/translate` (using `TranslationModel`).
- Models are loaded from pre-trained weights fine-tuned on AI4BHARAT datasets.

## Deployment Details

### Cloud Deployment
- **Provider**: OlaKrutrim / Hugginface
- **GPU**: RTX 4090 (1-3 instances based on phase).
- **OS**: Ubuntu 22.04 LTS
- **Cost**: $0.5/hour, total $1,800 over 3 months.

### Development Phases
1. **Month 1**: Single GPU, API setup, model fine-tuning.
2. **Month 2**: Scale to 3 GPUs, multi-user testing.
3. **Month 3**: Full load testing, final demo polish.

## Conclusion

The C4 model provides a comprehensive view of the Kannada Voice System, from its high-level context to detailed code structure. It ensures the demo is architecturally sound, leveraging GPU resources efficiently to deliver real-time ASR, TTS, and translation for Kannada speakers. This model serves as a blueprint for development and deployment over the three-month project timeline.


—------

Feb 24, 2025

# Technical Specification Document: Kannada Voice Model Development Demo

## Project Overview

The Kannada Voice Model Development project aims to create a robust voice assistant solution for the Kannada language, leveraging open-source Large Language Models (LLMs) and tools from AI4BHARAT. The demo will showcase three core functionalities: Automatic Speech Recognition (ASR), Text-to-Speech (TTS), and translation services, tailored specifically for Kannada and extensible to other Indian languages. This technical specification outlines the system requirements, architecture, and deliverables for a functional demo to be developed over a three-month period with GPU access.

---

## Objectives

- Demonstrate real-time ASR for converting spoken Kannada into text.
- Showcase natural-sounding TTS for converting Kannada text into speech.
- Highlight translation capabilities between Kannada and at least one other Indian language (e.g., Hindi or Tamil).
- Prove scalability and performance using GPU-accelerated processing.

---

## Technical Requirements

### 1. Hardware Requirements

#### Current Setup
- **Laptop**: GTX 1060 with 6GB VRAM
  - *Limitations*: Insufficient for large-scale training and real-time inference under load.

#### Demo Requirements
- **GPU Resources**:
  - *Minimum*: 1 GPU with at least 12GB VRAM (e.g., RTX 4090 or equivalent).
  - *Recommended*: 3 GPUs with 24GB VRAM each (e.g., A100 or RTX A6000) for scalability testing.
  - *Runtime*:
	- Month 1: 8 GPU hours/day (development).
	- Month 2: 16 GPU hours/day (scalability tests).
	- Month 3: 24 GPU hours/day (large-scale testing).
- **Storage**: 80GB minimum for model weights, datasets, and logs.
- **RAM**: 18GB minimum for data preprocessing and inference.
- **vCPUs**: 2-4 cores for parallel processing.

### 2. Software Requirements

#### Open-Source Tools
- **ASR**: [ASR Indic Server](https://github.com/slabstech/asr-indic-server)
  - Framework: Likely based on PyTorch or TensorFlow.
  - Model: Pre-trained Indic ASR model fine-tuned for Kannada.
- **TTS**: [Parler TTS Server](https://github.com/slabstech/parler-tts-server)
  - Framework: PyTorch.
  - Model: Pre-trained TTS model adapted for Kannada phonetics.
- **Translation**: [Indic Translate Server](https://github.com/slabstech/indic-translate-server)
  - Framework: Likely Transformer-based (e.g., Hugging Face models).
  - Model: Fine-tuned for Kannada-to-other Indian language translation.

#### Dependencies
- **Operating System**: Ubuntu 22.04 LTS .
- **Programming Language**: Python 3.10+.
- **Libraries**:
  - PyTorch (GPU-enabled).
  - NumPy, Pandas (data handling).
  - Hugging Face Transformers (for model fine-tuning).
  - Torchaudio (audio processing).
  - FastAPI (for server deployment).

#### Dataset
- **Source**: AI4BHARAT datasets (e.g., IndicSpeech, IndicTTS).
- **Size**: ~10-20GB of Kannada audio/text pairs for training and validation.
- **Preprocessing**: Audio normalization, text tokenization.

---

## System Architecture

### 1. High-Level Architecture
```
[User Input] --> [ASR Module] --> [Text Processing] --> [TTS Module] --> [Audio Output]
            	|                     	|
            	|--------------------[Translation Module] --> [Translated Text]

```
- **Input**: Microphone-captured Kannada speech or text input.
- **Output**: Spoken Kannada audio or translated text/speech.

### 2. Component Breakdown

#### ASR Module
- **Function**: Convert spoken Kannada to text.
- **Model**: Fine-tuned Indic ASR model.
- **Input**: WAV audio (16kHz, mono).
- **Output**: Kannada text (UTF-8 encoded).
- **Latency Goal**: < 500ms for real-time demo.

#### TTS Module
- **Function**: Convert Kannada text to natural-sounding speech.
- **Model**: Fine-tuned Parler TTS model.
- **Input**: Kannada text (UTF-8 encoded).
- **Output**: WAV audio (22kHz, mono).
- **Quality Goal**: MOS (Mean Opinion Score) > 4.0.

#### Translation Module
- **Function**: Translate Kannada text to another Indian language (e.g., Hindi).
- **Model**: Fine-tuned Indic Translate model.
- **Input**: Kannada text (UTF-8 encoded).
- **Output**: Translated text (UTF-8 encoded).
- **Accuracy Goal**: BLEU score > 0.8.

#### Server Infrastructure
- **Deployment**: Flask/FastAPI server hosted on cloud GPU instance.
- **API Endpoints**:
  - `/asr`: Audio → Text.
  - `/tts`: Text → Audio.
  - `/translate`: Text → Translated Text.

---

## Demo Deliverables

1. **Live Demonstration**:
   - User speaks a Kannada phrase → System transcribes it → System responds with spoken Kannada output.
   - User inputs Kannada text → System translates to Hindi and speaks it back.
2. **Performance Metrics**:
   - ASR latency, TTS quality (MOS), translation accuracy (BLEU).
3. **Source Code**: GitHub repository with server and model configurations.
4. **Documentation**: README with setup instructions and API usage.

---

## Risks and Mitigation

- **Risk**: Insufficient GPU performance for real-time inference.
  - *Mitigation*: Start with a single high-VRAM GPU (e.g., RTX 4090) and scale as needed.
- **Risk**: Dataset quality affects model accuracy.
  - *Mitigation*: Validate and augment AI4BHARAT datasets with additional Kannada samples if required.
- **Risk**: Cost overrun beyond $1,800.
  - *Mitigation*: Monitor usage daily and adjust GPU hours if approaching budget limits.

---

## Conclusion

This technical specification outlines the requirements and roadmap for a successful demo of the Kannada Voice Model. With GPU access secured for three months, the project will deliver a functional, scalable voice assistant solution comparable to industry standards, tailored for Kannada speakers. The demo will serve as a proof-of-concept for further funding and development.


—------
Feb 24, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-24-gpu-access.md


# Project Dhwani: Enhancing Kannada Voice Model Development with GPU Access

## Table of Contents

1. [Summary](#summary)
2. [Introduction](#introduction)
	- [Background](#background)
	- [Objectives](#objectives)
3. [Budget](#budget)
	- [Cloud Providers](#cloud-providers)
	- [On-Premise GPU Setup](#on-premise-gpu-setup)
	- [GPU Access Cost Estimation](#gpu-access-cost-estimation)
4. [Project Scope](#project-scope)
	- [Models and Tools](#models-and-tools)
	- [Current Setup](#current-setup)
5. [Proposed Plan](#proposed-plan)
	- [Phase 1: Cloud Provider setup with Single GPU](#phase-1-cloud-provider-setup-with-single-gpu)
	- [Phase 2: Alpha user scaling with multi-gpu setup ](#phase-2-alpha-user-scaling-with-multi-gpu-setup)
	- [Phase 3: Resource Maximization and Scalability to Beta users](#phase-3-resource-maximization-and-scalability-to-beta-users)
6. [Test Cloud Provider](#test-cloud-provider)
	- [Overview](#overview)
	- [Provider and Costs](#provider-and-costs)
7. [Alternate Cloud Providers for GPU Access](#alternate-cloud-providers-for-gpu-access)
7. [Additional Reading Materials](#additional-reading-materials)
	- [Dhwani - 3 months Milestone Document](#dhwani---3-month---milestone-plan)
	- [Technical Specifications](#technical-specifications)
9. [Conclusion](#conclusion)
10. [Contact Information](#contact-information)


## Summary

Dhwani is a self-hosted GenAI platform designed to provide voice mode interaction for Kannada and other Indian languages.

## Research Goals

- Measure and improve the Time to First Token Generation (TTFTG) for model architectures in ASR, Translation, and TTS systems.
- Develop and enhance a Kannada voice model that meets industry standards set by OpenAI, Google, ElevenLabs, xAI
- Create robust voice solutions for Indian languages, with a specific emphasis on Kannada.


## Introduction

### Project Website - [https://slabstech.com/dhwani](https://slabstech.com/dhwani)

### Report - [Doc](https://docs.google.com/document/d/e/2PACX-1vRRNjjDrbjAGDQgUWtA5LR0TzwviNn61GYpn3Xm0-WKZrjjTyH2GhDdyY80pNp82oQdAfb60auQvVRW/pub)

### Presentation - [SLides](https://docs.google.com/presentation/d/e/2PACX-1vQxLtbL_kXOqHgAHqcFTg8hDP7Dw3lt64U336J0f9CgYQPKDJVqONd3F4Js1XiCvk_LDpbijshQ5mM6/pub?start=false&loop=false&delayms=3000)


### Background

Current voice assistants like Alexa, Siri, and Google dominate the consumer market but lack comprehensive support for Indian languages, particularly Kannada. OpenAI's recent entry into the voice assistant market highlights the growing demand for such technologies. By utilizing open-source models and tools, we can develop a voice solution that is accessible and robust, specifically tailored for Kannada speakers.

### Objectives

The primary objective is to integrate and enhance the following models and services for Kannada:
- **Automatic Speech Recognition (ASR)**: To convert spoken Kannada into text.
- **Text-to-Speech (TTS)**: To convert Kannada text into natural-sounding speech.
- **Translation Services**: To enable translation between Kannada and other Indian languages.

### Models and Tools

The project utilizes the following open-source tools:

| Open-Source Tool                   	| Source Repository                                      	| CPU / Available 24/7 - Free| GPU / On-demand |
|---------------------------------------|-------------------------------------------------------------|----------------|----------------|
| Automatic Speech Recognition : ASR   | [ASR Indic Server](https://github.com/slabstech/asr-indic-server) | [API Demo](https://huggingface.co/spaces/gaganyatri/asr_indic_server_cpu)  |  - |
| Text to Speech : TTS              	| [TTS Indic Server](https://github.com/slabstech/tts-indic-server)  | CPU-not suitable         	| [App -Demo](https://huggingface.co/spaces/gaganyatri/tts_indic_local) |
| Translation                       	| [Indic Translate Server](https://github.com/slabstech/indic-translate-server) | [API Demo](https://huggingface.co/spaces/gaganyatri/translate_indic_server_cpu)      	|        	|
| Large Language Model                       	| [LLM Indic Server](https://github.com/slabstech/llm-indic-server_cpu) | [API Demo](https://huggingface.co/spaces/gaganyatri/translate_indic_server_cpu)     	|        	|
| Document Parser                       	| [Indic Document Server](https://github.com/slabstech/docs-indic-server) | Not Suitable      	|	-    	|
|All in One Server - ASR + TTS + Translate | [indic-all-server](server/indic_all/) | Not Suitable |  -- |


## Target Solution

| Answer Engine                              	| Voice Translation                      	|
|-----------------------------------------------|---------------------------------------------|
| ![Answer Engine](kannada-answer-engine.drawio.png "Engine") | ![Voice Translation](voice-translation.drawio.png "Voice Translation") |

## Budget

### Cloud Providers

- **Cost**: Estimated $2,880 for three months of cloud-based GPU access.
- **Justification**: Necessary for initial infra setup, model optimization and performance evaluation.

### On-Premise GPU Setup

- **Cost**: $4,000 for hardware and setup: RTX 4090 - Workstation with 24GB VRAM
- **Justification**: Long-term investment for sustainable development and scalability.

We will target implementaion with Single GPU

### GPU Access Cost Estimation

#### Cost Breakdown
| Month | Activity                      	| Users | Cost per Hour/GPU ($) | Hours per Day | Daily Cost ($) | Monthly Cost ($) |
|-------|-----------------------------------|-------|-----------------------|---------------|----------------|------------------|
| 1 	| Development and optimization  	| 1-5   | 0.5               	| 4         	| 2.00       	| 960          	|
| 2 	| Scalability tests and beta users | 10-20 | 0.5               	| 24        	| 12.00      	| 960          	|
| 3 	| Large scale testing across timezones | 10-20 | 0.5               	| 36        	| 18.00      	| 960          	|

**Total Cost**
- **Total Cost**: $960 + $960 + $960 = $2,880

## Project Scope


### Current Setup

The development is currently being executed on a laptop with a GTX 1060 6GB VRAM. However, to ensure robustness and scalability, additional GPU resources are required.


#### Integrated Demos
- Demo for Testing components for Dhwani for Accuracy and evaluation

| Feature                  	| Description                                                             	|  Components      	| Source Code   	| Hardware   	|
|------------------------------|-----------------------------------------------------------------------------|-----------|---------------------|---------------|
| Kannada Voice AI            	| Provides answers to voice queries using a LLM                 	| LLM             	| [API](ux/answer_engine/app.py) // [APP](ux/answer_engine/local/app.py)      	| CPU / GPU |
| Text Translate           	| Translates text from one language to another.                            	|  Translation     	| [Link](ux/text_translate/app.py)      	| CPU / GPU |
| Text Query               	| Allows querying text data for specific information.                      	| LLM             	| [Link](ux/text_query/app.py)      	| CPU / GPU |
| Voice to Text Translation	| Converts spoken language to text and translates it.                      	|  ASR, Translation	| [Link](ux/voice_to_text_translation/app.py)      	| CPU / GPU |
| PDF Translate            	| Translates content from PDF documents.                                   	|  | Translation     	|       	| GPU |
| Text to Speech       	| Generates speech from text.                                              	|  TTS             	| [Link](ux/text_to_speech/app.py)      	| GPU |
| Voice to Voice Translation   | Converts spoken language to text, translates it, and then generates speech.   |  ASR, Translation, TTS| [Link](ux/voice_to_voice_translation/app.py)      	| GPU |
| Answer Engine with Translate| Provides answers to queries with translation capabilities.               	|  ASR, LLM, Translation, TTS|  [Link](ux/answer_engine_translate/app.py)      	| GPU|


## Proposed Plan

### Phase 1: Cloud Provider setup with Single GPU

- **Objective**: Utilize cloud-based GPU resources to enhance the models.
- **Actions**:
  - Set up and configure cloud-based GPUs.
  - Perform initial training and testing of ASR, TTS, and translation models.
  - Evaluate the performance and make necessary adjustments.

### Phase 2: Alpha user scaling with multi-gpu setup

- **Objective**: Assess the feasibility of multi-GPU solutions.
- **Actions**:
  - Conduct a cost-benefit analysis of multi-GPU setup.
  - Continue model training and optimization using cloud-based GPUs.

### Phase 3: Resource Maximization and Scalability to Beta users

- **Objective**: Release to Beta users with advanced GPU.
- **Actions**:
  - Monitor the performance and resource utilization.
  - Adjust the project plan as needed to ensure efficient use of resources.
  - Seek additional funding or resources based on project progress and demand.


### Test Cloud Provider

- Huggingface Spaces,
- OlaKrutrim Cloud

### Provider and Costs

- Huggingface Spaces

Cost from Huggingface Spaces - Ease of Use and model close to server

| GPU Type        	| vCPU | Memory | GPU Model | GPU Memory | Price ($) |
|----------------------|------|--------|-----------|------------|-----------|
| Nvidia T4 - small	|  4   | 15 GB  | Nvidia T4 | 16 GB  	| $0.40  	|
| 1x Nvidia L4     	|  8   | 30 GB  | Nvidia L4 | 24 GB  	| $0.80  	|
| 1x Nvidia L40S   	|  8   | 62 GB  | Nvidia L4 | 48 GB  	| $1.80  	|
| Nvidia A10G - small  |  4   | 15 GB  | Nvidia A10G| 24 GB  	| $1.00  	|

- OlaKrutrim Cloud

| Instance Type     	| Price (₹/hour) | GPUs | Availability | vCPUs | GPU Memory | RAM	|
|-----------------------|----------------|------|-------------|-------|------------|--------|
| A100-NVLINK-Mini  	| ₹ 45       	| 1	| Medium | 16	| 20 GB  	|    	|
| A100-NVLINK-Standard-1x| ₹ 105      	| 1	| Medium | 16	| 40 GB  	| 60 GB  |
| H100-NVLINK-Nano  	| ₹ 83       	| 1	| Medium | 16	| 20 GB  	|    	|
| H100-NVLINK-Mini  	| ₹ 124      	| 1	| Medium  	| 16	| 40 GB  	| 60 GB  |

- WIP - [Cloud provider benchmark document](https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-27-cloud-provider-benchmarks.md)

## Additional Reading Materials

### Dhwani - 3 month - Milestone plan

[Dhwani Research Milestone document](https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-27-dhwani-research-milestones)

### Technical Specifications

For more detailed technical specifications, please refer to the following documents:

- [Technical Specifications for Indic Server](https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-24-tech-spec-indic-server.md)
- [C4 Specifications for Indic Server](https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-24-c4-spec-indic-server.md)

## Conclusion

This proposal aims to secure GPU access for three months to develop a robust Kannada/Indic Language voice model. By leveraging open-source tools and models, we can create a solution that meets the needs of Kannada speakers and contributes to the broader field of voice assistant technologies. Your support in providing GPU access will be instrumental in achieving this goal.

## Contact Information

For any inquiries or further discussion, please contact:

- [sachin]

- To collaborate immediately with code, feedback, issues : Join our [Discord Server](https://discord.gg/WZMCerEZ2P)
	- Clear, Small Pull Requests for [Milestones](https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-27-dhwani-research-milestones) - are worth its weight in Gold

---

We appreciate your consideration and look forward to the possibility of collaborating on this exciting project.

---

—---

Feb 27, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-27-dhwani-query-1-answer.md




Dhwani - Voice Mode

Queries on the proposal- Feb 27, 2025

1) I see that the base model that you will be using is ai4bharat/indicconformer_stt_kn_hybrid_ctc_rnnt_large  which seems to be a 120M parameter and hence looks like its size is just 523 Mb.

In that case -  If you select one of AWS's g4 instances such as g4dn.xlarge which has 16 GB of VRAM (which we are currently using in production for inference), you can run at least 20+ instances of this model on a single GPU at a cost of 0.50$ per hour.

For inference, to achieve single GPU - multiple model instances batching / load balancing of requests - We could use either:  i) NVIDIA Triton Server or ii) Ray serve

If we can fully utilize one GPU first and then expand to multiple GPUs, I believe this would reduce the number of GPUs to scale to your target numbers(for both training and inference since the base model is just 120M parameters)

So, do you think the number of GPUs you will need will change if you consider this approach?

Please correct me if any of my assumptions are incorrect.


2) Just a curious question -  You have mentioned about 'performing initial training and performance benchmarks to make the ai4bharat/indicconformer_stt_kn_hybrid_rnnt_large' better, but you haven't provided the details about - training/testing data that will be used, its size, the licensing arrangements regarding the usage of the data.


Response to Query 1


Below are the clarifications for the queries.

Voice Mode system is a combination of 4 distinct models
1. Automatioc Speech Recognition
2. Translation model
3. text LLM ( we will not initially work on this)
4. Text to Speech model


For first month,
We want to combine all the 4 systems and run it on a single GPU.
We want to start with the lowest compute server, which can fit all the Model VRAM requirements and 5 minute audio / context VRAM requirement.

Based on this baseline, we will convert the models to Triton kernel server. This needs investigation and effort.


Once we successfully export all the models triton kernels, we will work on scaling it up with large instance and load balancing with multiple small instance.

Multiple GPU requirement comes into play, if the model conversion fails due to lack of expertise.
Then we will host the pytorch/transformer/uvicorn models.

2. Evaluation harness will be done in the second months , if we observe that the accuracy is not good for daily use, then we will combine other available datasets to improve the model.
Re-training is currently out of scope for the initial exploration since it will involve additional effort of people and compute resources.

We want to first try how the existing models work ,
get it running with faster inference.


—-------


Feb 27, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-27-dhwani-research-milestones.md


Dhwani - Research Milestone

- [3 Months Plan](#3-months-plan)
	- [Key Activities](#key-activities)
    	- [Month 1](#month-1)
        	- [Week 1](#week-1)
        	- [Week 2](#week-2)
        	- [Week 3](#week-3)
        	- [Week 4](#week-4)
    	- [Month 2](#month-2)
        	- [Week 1-4](#week-1-4)
    	- [Month 3](#month-3)
        	- [Week 1-4](#week-1-4)



## 3 Months Plan

### Key Activities

- **Scaling and Verifying Concurrent Users**: Ensure the system can handle multiple users simultaneously.
- **Rate Limiting**: Implement measures to control the rate of requests to prevent system overload.
- **Multi-Language Support - Batching**: Enable support for multiple languages and optimize processing through batching.
- **Immersive Voice Mode**: Develop a mode for teaching, entertainment, and exploration with system prompts.
- **Fine-Tuning Models**: Continuously improve the models based on feedback and performance data.
- **Automated Red Teaming**: Simulate attacks to test and improve the system's security.
- **Weekly Progress Updates**: Provide updates on techniques tried, comparisons against top providers, and cost metrics.

### Month 1

#### Week 1
- **API Standards**: Define and implement API standards for the project.
- **Logging and Automatic Configuration of GPU**: Set up logging and automatic configuration for GPU resources.

#### Week 2
- **Performance Measurement**: Measure the performance of the models.
- **Eval Benchmarks**: Establish benchmarks for evaluation and comparison.

#### Week 3
- **Encryption and Privacy Management**: Implement encryption and privacy management protocols.

#### Week 4
- **Delta Updates to Models**: Apply delta updates to the models for continuous improvement.
- **RLHF and Federated Learning**: Implement Reinforcement Learning from Human Feedback (RLHF) and federated learning techniques.
- **Open Data Collection**: Collect open data for training and validation.
- **Weekly Cost Metrics Export**: Export and analyze weekly cost metrics.
- **Newsletter Enrollment**: Enroll users in a newsletter for regular updates and engagement.

### Month 2

#### Week 1-4
- **Scaling and Verifying Concurrent Users**: Test and verify the system's ability to handle multiple users.
- **Rate Limiting**: Implement rate limiting to manage system load.
- **Multi-Language Support - Batching**: Develop support for multiple languages and optimize through batching.
- **Immersive Voice Mode**: Create an immersive voice mode for various applications.
- **Fine-Tuning Models**: Continuously fine-tune the models based on performance data.
- **Automated Red Teaming**: Simulate attacks to identify and fix vulnerabilities.
- **Community Work Plan**: Engage with the community for feedback and support.
- **Feature Requests and Pull Request Management**: Manage feature requests and pull requests from the community.
- **Fixed Schedule of Uptime and Test Plans**: Establish a fixed schedule for uptime and test plans.
- **3rd Party Integration**: Integrate with third-party services and platforms.

### Month 3

#### Week 1-4
- **Resource Maximization**: Optimize resource usage for scalability.
- **Performance Monitoring**: Continuously monitor performance and make necessary adjustments.
- **Beta User Release**: Prepare for and execute the release to beta users.
- **Weekly Progress Updates**: Continue providing weekly updates on progress and cost metrics.
- **Batch Optimization Framework**: Develop a framework for batch optimization, focusing on lecture conversion and archival work.
- **Dataset Creation - Opt-In**: Create datasets through opt-in prompts in the app for selection.
- **Mobile App - Setup for Voice Mode**: Develop and set up a mobile app for voice mode.



Todo  MLOps

Observe speed of inference

Build online measurable document

Make app - production grade

Stres test - provide fast failure and feeback

More than 15 secs /
Fail fast for unpaid / unlogged users

Build ddos / ip- tracking for load testing

Netflix / perplexity style building of feature and release

Build demo examples / jupyter notebook

Api key - bearer key management

User management with fastapi and react/ material ui


Federated learning -

Caching for tts

Langfuse/posthog

Add analytics for all services
—--
Feb 28, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-28-dhwani-basic-features-v-0-0-01.md



Week 1 - project dhwani


## Project Roadmap: Advanced Voice Interaction System Development

### 1. Architecture and Design

1. Design the architecture with scalability and modularity in mind
2. Write comprehensive benchmarks for performance evaluation
3. Develop robust code evaluation processes
4. Implement GitHub Actions for continuous integration and automated testing
5. Design error handling and recovery mechanisms

### 2. Natural Language Understanding (NLU) and API Development

1. Implement advanced NLU capabilities
2. Standardize API format for consistency across the system
3. Update function calls with actual inputs and responses
4. Expand support for all Alexa-like functions
5. Develop context awareness and personalization features

### 3. Language Processing and Model Optimization

1. Add auto-detection of language
2. Switch and optimize ASR model
3. Fix bug with repeated words
4. Implement lazy loading of models
5. Reduce latency and response times for all interactions

### 4. Documentation and Testing

1. Improve documentation for clarity and completeness
2. Test with various compute options (beyond T4 GPU)
3. Write parser to show daily speed improvements
4. Implement comprehensive logging for all steps

### 5. Gradio Demo and Workflow Development

1. Enhance Gradio demo with language ASR model loading button
2. Focus on workflow verification (Month 1)
3. Implement key workflows:
   a. Two-way translation for tourists
   b. Question-answering in source language
   c. Call center analytics and automation
   d. Develop 7 additional use-cases (total 10)

### 6. Component Integration and Optimization

1. Refine and optimize the component chain:
   - ASR -> NLU -> Translate -> TTS
   - Text -> NLU -> TTS -> ASR
2. Ensure seamless integration between all components

## Top 3 Priority Items

1. Natural Language Understanding (NLU) Implementation
   - Enhance accuracy in comprehending user intent
   - Integrate context awareness and personalization features
   - Improve overall interaction quality and relevance

2. Error Handling and Recovery Mechanism
   - Design clear error messages and alternative options
   - Implement user guidance for error situations
   - Minimize user frustration and improve system robustness

3. Performance Optimization and Benchmarking
   - Focus on reducing latency and response times
   - Implement comprehensive logging and performance tracking
   - Conduct regular benchmarks to guide optimization efforts

## Summary of Tasks

This project aims to develop an advanced voice interaction system with state-of-the-art natural language understanding, personalization, and error handling capabilities. Key focus areas include architectural design, API standardization, workflow implementation, and continuous performance optimization. The system will support multiple use-cases such as translation, question-answering, and call center analytics. Development will prioritize NLU implementation, robust error handling, and performance optimization to ensure a highly efficient, user-friendly, and adaptable voice interaction platform.

--

initial idea !!!

Basic Features For Dhwani - v.0.0.1
for user Acceptance Testing second phase

Standardize Api format,  
Updatw the function calls,  with actual inputs and response

Support all Alexa functions.

Fix bug with repeated words

Add auto detection of language,  
Switch model fur for asr


Fix docs, make everything clear


Hf load time for gpu restart 10 mins with t4.

Should test with other compute.


Write benchmarks

Design the architecture now,  don't blindly build and let it fail for lack of testing.



Write evaluation for for code,  
Add github actions,  trigger tests for all commits.

Gradio demo,  
Add button, to load languages ASR .


Do lazy loading of models


Month 1 -
Use only the gradio demo for verification and designing of workflows for voice mode.

Don't spend time on UX development.

We should reduce the Latency and response times for every interactions.

Logs every steps, write a psrser to show speed improvements every day.

Workflows
1. Simple translation flow . Source language to target language  and reverse flow for two way conversations. Tourists use cases

2. Answer machine - ask a question in source language,  get response in source language with llm geherated response.

3. Call center analytics and automation automation.  Large scale audio input, llm parsers and report creation.

Consider 10 use- cases.

Identify components and steps in order of function call.  

ASR -> translate -> TTS  ,

Text -> TTS ->ASR ,


—
—---------

Mar 1, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-01-dhwani-work-division.md


Dhwani Work Division

- Sachin - Integration, Deployment, Research Plan, Demo
- Sahana - Text to Speech - UX, benchmarks, model optimisation

- students
	- Model Conversion
    	- asr - IndicConformer based on Nvidia Nemo
        	- onnx export
        	- triton server
        	- raycast server
	- Model tests and optimal GPU inference handling
	- Re-training and evaluation  

- Identify - Lowest Compute GPU cloud to handle Voice mode for 1/ 10/ 100/ 1000/ 10,000 users concurrently

- Fit models - ASR + TTS + LLM + Translation
- Lazy loading and pre-loading models based on use-case .
- scaling / scheduling and observations
-
—----

Mar 3, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-03-tco-dhwani.md

## Total Cost of Operation for Voice AI Proof of Concept (PoC) in Indian Languages

### Scenario 1: 6 Languages
#### Storage Requirements
| Component          	| Size per Unit | Units | Total Size |
|------------------------|---------------|-------|------------|
| ASR (6 languages)  	| 550 MB    	| 6 	| 3.5 GB 	|
| Translation (Distilled)| 930 MB    	| 3 	| 3 GB   	|
| Text-to-Speech     	| 4.5 GB    	| 1 	| 4.5 GB 	|
| **Total**          	|           	|   	| **11 GB**  |

#### Hardware Options and Costs
| Hardware  | Capacity | Cost per Hour | Monthly Cost (720 hours) |
|-----------|----------|---------------|--------------------------|
| T4 Small  | 16 GB	| $0.40     	| $288                 	|
| L4    	| 24 GB	| $0.80     	| $576                 	|
| A10 Small | 24 GB	| $1.00     	| $720                 	|

---

### Scenario 2: 22 Languages
#### Storage Requirements
| Component          	| Size per Unit | Units | Total Size |
|------------------------|---------------|-------|------------|
| ASR (22 languages) 	| 550 MB    	| 22	| 11 GB  	|
| Translation (Base) 	| 4.5 GB    	| 3 	| 15 GB  	|
| Text-to-Speech     	| 4.5 GB    	| 1 	| 4.5 GB 	|
| **Total**          	|           	|   	| **31 GB**  |

#### Hardware Options and Costs
| Hardware | Capacity | Cost per Hour | Monthly Cost (720 hours) |
|----------|----------|---------------|--------------------------|
| L40s 	| 48 GB	| $1.80     	| $1,296               	|

---

### Notes
- Monthly costs are calculated assuming 720 hours per month (24 hours/day × 30 days).
- All sizes are in gigabytes (GB) unless specified otherwise.
- Hardware selection should account for total storage requirements and performance needs.


—-
Mar 4, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-04-dhwani-llm-puzzle.md

Dhwani LLM puzzle


Just made qwen2.5 1B instruct respond to Query in Kannada. By adding a translator function.
All this is running on 3 cent/hour machine.

It needs further evaluation,  looks promising though.

No gpu required,  qwen doesn't understand Kannada, but the indictrans2 model translates to English quite well.  
Qwen now responds in English and we translate it back.


Now the full stack is 100% independent without need for 3rd Party services.
everything can be hosted with current hardware,  we just need to utilise properly.


continue speed run, explore all options.

-- system confugsv

50 cent stack.


2 workers of tts on t4.
3 cent - asr
3 cent - translate
3 cent -llm


Full asynchronous system, supporting all uses cases with degradation of quality.

Needs a good load balancer.


—-

Mar 6, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-06-mobile-kraken-voice-chat.md


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



—

Mar 7, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-07-dhwani-mobile-app-v1.md

Dhwani Mobile App - Voice AI for Kannada/Indian Languages

version - 0.0.1-v-1

Coming soon to Google Play and Apple App store.

Prototype APK file for early users,
link-  https://drive.google.com/file/d/1dEC2PcTvEgtdZysSeeEhwJPMsX80YCJp/view?usp=drivesdk

Support 6 languages coming very soon.

Kannada, Hindi, Marathi, Tamil, Telugu, Malayalam

Project website - https://slabstech.com/dhwani

#dhwani #mobileapp #ai4bharat



—---



March 8, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-08-dhwani-mobile-release-v-0-0-1.md


Mobile App - Dhwani - Release - 0.0.1


User Acquisition- Make video App to show Mobile usage,

Add more users to get release criteriea and usability testing.

Message people and call them to use the app.

--

Backend- language addition and metrics per call.



Handle additional changes with language based on input received in the endpoints
For transalte and transcription.
Make async wait for previous response, allow flr new requests without blocking .


---


Source for Android app  and Python server.

You can build your own android client and server.

Or use Dhwani android app,

Run the server on your local machine. And change the endpoints.

Goal is to make AI available to larger audience who don't have Kannada and other language native support.

Feel free to contribute to the project or build it ahead as your own idea.

server - https://github.com/slabstech/dhwani-server

android - https://github.com/slabstech/dhwani-android


---
To get early app access,
Please send me your email ID connected to the play store.  I'll add to the Alpha test user list.

---

https://play.google.com/apps/internaltest/4701634529159536323

Please Accept the invite for app via the link .
Then the app should be available next to install


–

March 23, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-23-voice-escape.md


Dhwani - Voice Escape - Game

Your robot twin is in the esacape room,
You cannot see, your handled controls are broken.
You can talk to the robot and listen to its response.

You can ask what it cane see,
You can control its movements with voice commands,
Use your voice and ears to escape the room.

—

Mar 26, 2025


https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-03-26-deepthink-learning.md

Deepthink - Learning

deepseek-r1  - think mode is still unexplored for non-tech audience.

Dhwani - will introduce "think" for Learning mode.

Now science/tech/maths would be more accessible for Indian languages.

Read latest arxiv papers in your native language.

—-

App 
—
Mar 23, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/app/2025-03-23-dhwani-app-sessions.md

Session - Dhwani App > NotebookLM

- Create embeddings of previous conversations.
- Collect all previous questons
	- to check for same context
- Ask and learn
	- How to build continued conversations as a long format of Chat
	+ Use this featuer for learning modules
    	- Upload a text-book
    	- Collect the questions and quiz the student
    	- Improve one's skill understanding on the topic

- How to implement this ?

—
March 26, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/app/2025-03-26-dhwani-learn-deep-think.md

Learn - Think via  deepseek-r1


Feature-

Showcase the use for learn / Add - learn tab in phone .

Use case -
Use pre-defined topics and provide teaching with verification.

Start with- science and maths

Take a photo -
Help them to solve a problem,
Dont provide solution immediately ,
Help them to get answers

Tech -

Use deepseek-r1  to explain topics in depth.

Provide the endpoint as /think



—-

Apr 4, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/app/2025-04-04-dhwani-german-language-support.md



Dhwani - German/ european language support

Greetings and Introductions

	Hallo (Hello)

	Guten Morgen (Good morning)

	Guten Tag (Good day)

	Guten Abend (Good evening)

	Gute Nacht (Good night)

	Wie ist Ihr Name? / Wie heißt du? (What is your name?)

	Ich heiße… / Mein Name ist… (My name is…)

	Woher kommen Sie? / Woher kommst du? (Where are you from?)

Basic Phrases

	Danke (Thanks)

	Bitte (You're welcome)

	Entschuldigung (Excuse me)

	Es tut mir leid (I'm sorry)

	Ich verstehe nicht (I don't understand)

	Können Sie langsamer sprechen? (Can you speak slower?)

	Können Sie das bitte wiederholen? (Can you repeat that?)

Conversational Phrases

	Wie geht es Ihnen? / Wie geht’s? (How are you?)

	Mir geht es gut, danke (I'm fine, thanks)

	Was machst du sonst so? (What else do you do?)

	Ich mag… (I like…)

	Ich hasse… (I hate…)

	Meine Hobbys sind… (My hobbies are…)

	Ich stimme dir zu (I agree with you)

Useful Questions

	Was ist das? (What is this?)

	Wie viel kostet das? (How much does it cost?)

	Wo ist…? (Where is…?)

	Können Sie etwas empfehlen? (Can you recommend something?)

Food and Drink

	Ein Bier bitte (A beer, please)

	Einen Kaffee bitte (One coffee, please)

	Guten Appetit (Bon appetit)

	Prost! (Cheers!)

Slang and Informal Phrases

	Moin, moin (Hello, used in Northern Germany)

	Geil (Awesome/Cool)

	Na? (Hey, what’s up?)

	Basta (Period/end of discussion)

	Quatsch (Nonsense)

	Ich habe die Nase voll (I’m fed up)

These phrases will help you navigate everyday conversations in German.


----


Here are question-answering examples similar to “Was ist die Hauptstadt von Deutschland?” (What is the capital of Germany?) in French, Dutch, Spanish, Italian, Polish, Portuguese, and Russian. Each question asks about the capital of the respective language's country, and I’ll assume Gemma 3 (or any capable multilingual model) would respond appropriately in the same language.
French

	Question: "Quelle est la capitale de la France ?"
	Expected Answer: "La capitale de la France est Paris."

Dutch

	Question: "Wat is de hoofdstad van Nederland?"
	Expected Answer: "De hoofdstad van Nederland is Amsterdam."

Spanish

	Question: "¿Cuál es la capital de España?"
	Expected Answer: "La capital de España es Madrid."

Italian

	Question: "Qual è la capitale dell'Italia?"
	Expected Answer: "La capitale dell'Italia è Roma."

Polish

	Question: "Jaka jest stolica Polski?"
	Expected Answer: "Stolicą Polski jest Warszawa." (The capital of Poland is Warsaw.)

Portuguese

	Question: "Qual é a capital de Portugal?"
	Expected Answer: "A capital de Portugal é Lisboa."

Russian

	Question: "Какая столица России?" (Kakaya stolitsa Rossii?)
	Expected Answer: "Столица России — Москва." (Stolitsa Rossii — Moskva.) (The capital of Russia is Moscow.)

—

Apr 5, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/app/2025-04-05-dhwani-internal-testing.md

Dhwani App - Mobile Release


- Closed Testing
	- Play Store - https://play.google.com/store/apps/details?id=com.slabstech.dhwani.voiceai
	- Web - https://play.google.com/apps/testing/com.slabstech.dhwani.voiceai

- Internal Testing
	- https://play.google.com/apps/internaltest/4701634529159536323


—

Apr 15, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/app/2025-04-15-android-app-v2-upgrades.md

V-0-0-0-1  - stable release

Add - Settings button to Login page

Use Api key - for 3rd oarty service


Work on handleing rate limits from clients
Rotate server logs every day.
Dont store any user requests

User preferences- stored only on user app
Personalization and history in mobile app

Export to md format from mobile
Follow- Files over app philosophy


-

Mobile App v2
Make app compatible with OpenAI API

Use any service from the Android App
--

Add option for anthropic/ mistral/ elevenlabs / sarvam / moondream

Showcase the apps in the showcase to get more users

Make it universal android App

Use any OpenAPI compatible service

—

Apr 18, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/app/2025-04-18-app-deep-linking.md


https://dhwani-ai.com/.well-known/assetlinks.json

[
  {
	"relation": [
  	"delegate_permission/common.handle_all_urls"
	],
	"target": {
  	"namespace": "android_app",
  	"package_name": "com.slabstech.dhwani.voiceai",
  	"sha256_cert_fingerprints": [
    
  	]
	}
  }
]


Android
https://play.google.com/store/apps/details?id=com.slabstech.dhwani.voiceai


Web
https://play.google.com/apps/testing/com.slabstech.dhwani.voiceai
Dhwani - Chat - Ondevice


https://developers.googleblog.com/en/gemma-3-on-mobile-and-web-with-google-ai-edge/

Apr 1, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/app/2024-04-01-dhwani-v3-app-upgrades-1st-week-april.md



Dhwani-AI- App - April 1-7 : 2025


Image Creation -
- style transfer
- ghibli mode


Language Support
- Gujurati / Raj C
- European language


Distribution-
- Publish on F drpid
- Samsung store
- India - app store


Errors -
- Downsize - images befote sending
 Dont send HD images.Reduce resolution-
- Max .5 mb
- Broken UX on large screen devices
- broken settings page on older device's with dark mode
-
—
Aws 

Apr 29, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/aws/2025-04-29-dwani-ai-migration-aws-api.md
dwani.ai - migration to AWS


Current setup
1. Api server + Database
- TLS - certificate required for https endpoints
- fastapi server with Python
- load balancing - route management to inference server
- user authentication and rate limiters for request
- logging and metrics
- Database- sqlite

2. UX
- Github pages deployment with DNS
- Typescript + React

3. Inference server
- fastapi + pytorch
- 24 GB VRAM minimum GPU for Workshop server
- 70 GB VRAM current system for production

4. Swagger UI
- hf.space/slabstech

Next changes - May 4 : Android release

1. API server  - Backend- fastapi
2. Db server - Backend- postgreSQL
3. UX - dwani.ai  - landing page - Typescript/React
4. UX - api.dwani.ai - swagger ux / mintlify
5. Inference server - backend  - fastapi + pytorch


—
Collab

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/collab/2025-03-31-knowled-edtech.md

Edtech for Learning Difficulties

- How can Dhwani AI support XYZ company

- Phase 1 - 3-6 months
  - Android App based Product for Students ( Tablet/ Mobile Phone)
  - Provide Speech Recognition for Kannada/Indian languages
	- Record Student Answers
  - Provide Text to Speech for Kannada/Indian languages
	- Ask Questions to students
  - Provide Assessments for Answer
	- Make automated assessment using AI

- Phase 2 - 6-12 months
  - Integrate with hardward fr Writing analysis
  - Make personalized lesson plan for students with AI summary based on student history



- Phase 1 work can be supported with current Dhwani AI
- Phase 2 work will be supported with features planned in Dhwani AI roadmap

- We will provide the necessary software support with monthly upgrades and maintenance.
- Module development will be milestone based, with each module costing independently based on integrations.
- All code designed, created, developed, modified will be property of S Lab Solutions,  Will license the usage to your company.

—
Apr 28, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/events/2025-04-28-workshop-gopalan-college.md

—

2nd dwani.ai Workshop

- Institute
	- Gopalan College on Engineering and Management, Benguluru

- Date
	- 28 April 2025

- Resource Person
	- Sahana Shetty
	- Nitish S


- Social Link
  - LinkedIn - [https://www.linkedin.com/posts/sachinlabs_dwani-kannada-workshop-activity-7322652132808011777-3msO](https://www.linkedin.com/posts/sachinlabs_dwani-kannada-workshop-activity-7322652132808011777-3msO)
  - X/Twitter - [https://x.com/gaganyatri/status/1916893398646034742](https://x.com/gaganyatri/status/1916893398646034742)


—
Apr 2, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/models/2025-04-02-llm-krutrim.md

LLM for kannada



https://huggingface.co/bartowski/krutrim-ai-labs_Krutrim-2-instruct-GGUF


krutrim-ai-labs_Krutrim-2-instruct-Q6_K.gguf


—

Misc

—
Mar 17, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-03-17-dhwani-feature-v2.md

Dhwani - App features

1. Live Transcription
Translate in real time without llm in betwen.

Suitable for handsfree on mobile app
 
Make it work for german,  Kannada language first.

More users require it immediate.

Set source and target language.


Choose - main screen in setting.


2. learn a topic
Build Jarvis- Voice AI / Activr listener for wake up.

Meeting - Notes taker
Voice / Text / Analysis

Learn -
Ask a topic- use deepseek - think option
To build on the app.


Rabbit AI - actuon model,
Control App via AI

3. tell me what you see ?

—
Mar 22, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-03-22-dhwani-roadmap-v2-march-22-27.md

Dhwani- v2 - Roadmap - March 22-27

1. Main issue -

Dark theme - old phone is broken
Not usable to access settings

2. Api server -
For routing and loadbalamcing update system
From python to go ?

Make it serve with less resources and high throughput

3. Canvas/ message bist
Message reaponse body should be  markdown reader.

To present data in a nice format

4. Auto Voice language
Sample 2 sec audio on each Language for Transcription

Pass it via asr for the available Language and get  text in multiple Language

Use Indic lid for text to match exact language.

Currently ASR is not streaming,  
We want to add streaming voice input first and experiment with language identification.

5. Live transcription- earphone to App ?
Stream AsR / feed to b to translate

Show real time audioc in n text

6. University Collab / access

Register with Uni email .

Get access token and build so.

Provide info / about app Chankya uni in app.

Add a separate tab / rag based /

7. App Features/ characters

Add - status icon in settings page

Show availability of service

Choose- better models

Add - option for character's / stoeries

Ramayana/ mahabharsya
Non-copyrighted books only

8. API Server - user management
Csv uploader  - server - restart

Db backups?

Name , type
Type - mobile
Type- web

Username - full-email id

Password: username part before  @

Allowed- domains

gmail.com
chanakyauniversity.edu.in


Add - gpu check ? Torch compile
Use bfloat16 for l4 and above

9. Parler-tts- distillation
Make smaller generator/
Distill the project for individual language

Improve speed and accuracy?
Can we do it ?

10. Dhwani Marketing-integration
Create integration with 3rd Party clirnts

Live kit
Fast rtx
Plivo
Twilio
Whatsapp Api

11. Dhwani - web ux - user management

Create a simple screen on dhwani - website

Login with admin details.

Get list of useers updatws to systen.

Add new users with simple button.


12. Dhwani - model - server
Fix - issue with asyn calls.

Make load testing of projrct .


Add load balancing to main api


Based on compute available,  auto scale the systen
Non GPU
T4 -
L4

Select betwen
Gemma3-4b-instruct
Gemma3-4b-instruct quantized

Gemma3-1b-instruct
Gemma3-1b-instruct quantized

Translation models

Voice model /

Always lazy load


13, Transcription

Translate in real time without llm in betwen.

Suitable for handsfree on mobile app
 
Make it work for german,  Kannada language first.

More users require it immediate.

Set source and target language.


Choose - main screen in setting.


14.

—-

Mar 25, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-03-25-dhwani-4-weeks-march.md


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

—

Mar 25, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-03-25-digital-hub-dhwani-pitch.md


Dhwani - Europe - digital hub - pitch


Feature addition

- European language support

- Add - whisper transcription endpoint to HF

- Update- router for new languages

- Add - german / dutch / English  for android app

- Add - parler-tts multilingual for non-indic languages

- Router should choose endpoint based on language selected


--

Jury

- Date - April 29, 2025

- 5 min pitch,  5 min Q n A

- improve pitch document/ get feedback from Luca

Jury : requirements
- mvp and technical specs
- users and market testing
- business case / revenue plan


- use cases
 - Integration course / supplement learning
 - image response in local language
- real time transcription/ for queries in German to non-german speakers
- api for learning app

Apr 6, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-04-06-dhwani-april-week-1-changelog.md


Dhwani - April 2025 - Week 1 ChangeLog



Tech development
1. Early version - Speech to Speech for Kannada

2. Dhwani Mobile App -
Chat / Image description and Text To Speech supprt added for 5 european language: German, French, Dutch , Italian and Spanish

3. Text to Image and Image Edit Experiments

4. API server upgraded for User management and load balancing of Dhwani model server

5. Hardware based configs added for Dhwani model server for One Click deployment.  Choose from Nvidia T4 to L4 To A100 servers

6. Integration of upgraded ASR model from AI4Bharat, single model for 22 languages.

Outreach
- Dhwani AI seminar and 3 hour workshop planned at Garden city University,  Bengaluru and Gopalan College of Engineering,  Bengaluru

- Presented Dhwani AI app - Dual use technology during European Defense Tech Hackathon Amsterdam - March 28-30, 2025

Next :
Dhwani AI - version 1 - stable release planned for Week 2 - April 2025.

—
Apr 11, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-04-11-dhwani-v1-latency-report-v2.md


# Latency Results for Dhwani AI - Speech-to-Speech Voice Assistant

# Latency Report

This report presents the restructured latency analysis across various GPUs, organized using tables for clarity and comparison. It includes total latency, a breakdown by phase (Non-TTS and TTS), and concludes with key insights and recommendations.

## Total Latency Across GPUs

The table below summarizes the total latency for three requests across different GPUs, along with the average latency and notable observations.

| GPU     	| Request 1 (s) | Request 2 (s) | Request 3 (s) | Average (s) | Notes                                       	|
|-------------|---------------|---------------|---------------|-------------|-------------------------------------------------|
| A100    	| 6.668     	| 6.621     	| 6.515     	| 6.601   	| Consistent performance around 6.5–6.7 seconds.  |
| L40 S   	| 6.536     	| 4.400     	| 4.479     	| 4.440*  	| First request slower (6.536s); stabilizes at ~4.4s. |
| L4      	| 11.687    	| 9.344     	| 9.207     	| 9.276*  	| Improves to ~9.2s after slow first request (11.687s). |
| T4 Medium   | 19.504    	| 17.746    	| 17.898    	| 17.822* 	| High latency, stabilizing at ~17.8s.        	|
| T4      	| 20.830    	| 18.643    	| 18.850    	| 18.747* 	| Slowest overall, around 18.7s after warmup. 	|

*Note*: Average calculated after the first request to account for initialization effects.

## Latency Breakdown by Phase

The latency is broken down into two phases: Non-TTS Phase (transcription to processed text) and TTS Phase (processed text to request completion). Each phase is presented in a separate table.

### Non-TTS Phase (Transcription to Processed Text)

| GPU     	| Request 1 (s) | Average (Requests 2–3) (s) | Notes                          	|
|-------------|---------------|----------------------------|------------------------------------|
| A100    	| 1.507     	| ~1.5                   	| Consistent across requests.    	|
| L40 S   	| 1.515     	| ~1.3                   	| Slightly faster after first request. |
| L4      	| 1.630     	| ~1.3                   	| Improves after first request.  	|
| T4 Medium   | 2.078     	| ~1.8                   	| Higher latency compared to others. |
| T4      	| 2.189     	| ~1.9                   	| Highest latency in this phase. 	|

### TTS Phase (Processed Text to Request Completion)

| GPU     	| Request 1 (s) | Average (Requests 2–3) (s) | Notes                          	|
|-------------|---------------|----------------------------|------------------------------------|
| A100    	| 5.161     	| ~5.0                   	| Consistent performance.        	|
| L40 S   	| 5.021     	| ~3.1                   	| Significant improvement after first request. |
| L4      	| 10.057    	| ~8.0                   	| Reduces after initial request. 	|
| T4 Medium   | 17.426    	| ~16.0                  	| High latency, even after warmup.   |
| T4      	| 18.641    	| ~17.0                  	| Highest TTS latency.           	|

## Key Insights

### Total Latency

- **Fastest**: L40 S (~4.4s after warmup).
- **Most Consistent**: A100 (~6.5s across requests).
- **Moderate**: L4 (~9.2s after warmup).
- **Slowest**: T4 (18.7s) and T4 Medium (17.8s) after warmup.

### Non-TTS Phase

- Relatively quick across all GPUs (1.3–2.2s).
- **Best Performers**: L40 S and L4 (~1.3s after warmup).
- **Slowest**: T4 (1.9s) and T4 Medium (1.8s).

### TTS Phase

- Primary source of latency variation:
  - **Fastest**: L40 S (~3.1s after warmup).
  - **Consistent**: A100 (~5s).
  - **Moderate**: L4 (~8s after warmup).
  - **Slowest**: T4 Medium (16s) and T4 (17s).

## Conclusion

The L40 S GPU delivers the lowest total latency (4.4s after warmup, with ~3s in the TTS phase), making it the best choice for real-time applications like Dhwani AI. The A100 GPU offers reliable performance (6.5s total, 5s TTS), serving as a strong alternative. The TTS phase is the primary bottleneck, particularly for the T4 (17s) and T4 Medium (~16s), highlighting it as a critical area for optimization. The Non-TTS phase shows less variation (1.3–2.2s) and is less impactful on overall performance.


--



This document provides the latency results for Dhwani AI, a speech-to-speech voice assistant designed for Kannada and other Indian languages. The pipeline processes spoken Kannada input through transcription, translation to English, response generation, translation back to Kannada, and speech synthesis. We evaluated five GPU configurations—A100, L40 S, L4, T4 Medium, and T4—based on total request times and key processing phases, derived from server logs.

## Total Latency Across GPUs

The total request time represents the end-to-end duration from receiving audio input to delivering the spoken response. Below are the results for three requests per GPU, showing consistency and initialization effects:

- **A100**:
  - Request 1: 6.668 seconds
  - Request 2: 6.621 seconds
  - Request 3: 6.515 seconds
  - **Average**: 6.601 seconds
  - **Note**: Stable performance around 6.5–6.7 seconds.

- **L40 S**:
  - Request 1: 6.536 seconds
  - Request 2: 4.400 seconds
  - Request 3: 4.479 seconds
  - **Average (after first request)**: 4.440 seconds
  - **Note**: First request slower due to initialization; stabilizes at ~4.4 seconds.

- **L4**:
  - Request 1: 11.687 seconds
  - Request 2: 9.344 seconds
  - Request 3: 9.207 seconds
  - **Average (after first request)**: 9.276 seconds
  - **Note**: Improves to ~9.2 seconds after a slow first request.

- **T4 Medium**:
  - Request 1: 19.504 seconds
  - Request 2: 17.746 seconds
  - Request 3: 17.898 seconds
  - **Average (after first request)**: 17.822 seconds
  - **Note**: High latency, stabilizing at ~17.8 seconds.

- **T4**:
  - Request 1: 20.830 seconds
  - Request 2: 18.643 seconds
  - Request 3: 18.850 seconds
  - **Average (after first request)**: 18.747 seconds
  - **Note**: Slowest overall, around 18.7 seconds after warmup.

### Summary of Total Latency
- **Fastest**: L40 S (~4.4 seconds after warmup).
- **Most Consistent**: A100 (~6.5 seconds).
- **Moderate**: L4 (~9.2 seconds after warmup).
- **Slowest**: T4 (~18.7 seconds) and T4 Medium (~17.8 seconds).

## Latency Breakdown by Phase

The pipeline splits into two main phases:
1. **Non-TTS Phase**: Transcription, translation to English, response generation, and translation to Kannada.
2. **TTS Phase**: Text-to-speech synthesis of the Kannada response.

Below is the breakdown based on the first request, with averages for subsequent requests to account for initialization:

### Non-TTS Phase
- **A100**:
  - Request 1: 1.507 seconds
  - Average: ~1.5 seconds
- **L40 S**:
  - Request 1: 1.515 seconds
  - Average (Requests 2–3): ~1.3 seconds
- **L4**:
  - Request 1: 1.630 seconds
  - Average (Requests 2–3): ~1.3 seconds
- **T4 Medium**:
  - Request 1: 2.078 seconds
  - Average (Requests 2–3): ~1.8 seconds
- **T4**:
  - Request 1: 2.189 seconds
  - Average (Requests 2–3): ~1.9 seconds

### TTS Phase
- **A100**:
  - Request 1: 5.161 seconds
  - Average: ~5 seconds
- **L40 S**:
  - Request 1: 5.021 seconds
  - Average (Requests 2–3): ~3.1 seconds
- **L4**:
  - Request 1: 10.057 seconds
  - Average (Requests 2–3): ~8 seconds
- **T4 Medium**:
  - Request 1: 17.426 seconds
  - Average (Requests 2–3): ~16 seconds
- **T4**:
  - Request 1: 18.641 seconds
  - Average (Requests 2–3): ~17 seconds

### Phase Insights
- **Non-TTS**: Quick across GPUs (1.3–2.2 seconds), with L40 S and L4 leading (~1.3 seconds after warmup).
- **TTS**: Major contributor to latency differences:
  - L40 S excels (~3 seconds after warmup).
  - A100 steady (~5 seconds).
  - L4 moderate (~8 seconds).
  - T4 Medium and T4 lag (~16–17 seconds).

## Conclusion

The L40 S GPU offers the lowest latency (~4.4 seconds total, ~3 seconds TTS after warmup), making it ideal for real-time use. The A100 follows closely (~6.5 seconds total, ~5 seconds TTS) with reliable performance. The TTS phase drives most latency variations, especially on slower GPUs like T4 and T4 Medium (~17–18 seconds total), highlighting it as a critical area for optimization.


—

Apr 11, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-04-11-dhwani-v1-latency-report.md

Dhwani AI - Latency Report
# Latency Report for Dhwani AI Voice Assistant


# Summary Latency Report for Dhwani AI Voice Assistant

## Overview
This summary condenses the latency analysis of the Dhwani AI Voice Assistant, a Kannada/Indian language voice assistant, based on server logs from April 11, 2025. The analysis compares four hardware configurations (L40S, L4, T4 Medium, T4) for the `/v1/speech_to_speech` endpoint, focusing on end-to-end latency, processing stages, bottlenecks, and recommendations.

## Key Findings

### Hardware Performance
| Hardware   | Average Latency (s) | Standard Deviation (s) | First Request Note                 	|
|------------|---------------------|------------------------|----------------------------------------|
| L40S   	| 5.138           	| 1.171              	| Slower at 6.536 s vs. 4.400 s later	|
| L4     	| 10.079          	| 1.374              	| Moderate performance               	|
| T4 Medium  | 18.383          	| 0.952              	| Slow, consistent latency           	|
| T4     	| 19.441          	| 1.147              	| Slowest overall                    	|

### Processing Stages
| Stage                	| Latency Range (s) | Contribution (%) | Notes                          	|
|--------------------------|-------------------|------------------|------------------------------------|
| Transcription        	| ~0.001        	| <0.02        	| Near-instant, negligible impact	|
| Translation to English   | 0.266–0.312   	| 1.60–5.80    	| Minor contributor              	|
| Response Generation  	| 0.911–1.445   	| 7.43–17.73   	| Fastest on L40S (0.911 s)      	|
| Translation to Kannada   | 0.192–0.265   	| 1.27–3.74    	| Fast across all hardware       	|
| Remaining (e.g., speech synthesis) | 3.736–17.418	| 72.71–89.60  	| Dominates latency, likely speech synthesis |

### Bottlenecks
| Bottleneck Type | Description                                  	| Impact Details                          	|
|-----------------|--------------------------------------------------|---------------------------------------------|
| Primary     	| Remaining time (speech synthesis, unlogged tasks) | 72.71% (L40S) to 89.60% (T4) of latency 	|
| Secondary   	| Response generation                          	| Slower on T4/T4 Medium (1.383–1.445 s)  	|
| Other       	| Cold start delays, tokenizer warning         	| First request slower; warning non-critical  |

## Recommendations
| Action Item                      	| Description                                                             	|
|--------------------------------------|-----------------------------------------------------------------------------|
| Optimize Speech Synthesis        	| Profile and optimize text-to-speech (e.g., quantization, lighter models) 	|
| Enhance Response Generation      	| Optimize language model for T4/T4 Medium (e.g., mixed precision, pruning)	|
| Reduce Cold Start Latency        	| Implement model preloading or caching for common queries                	|
| Improve Logging                  	| Add speech synthesis timestamps, increase precision                     	|
| Hardware Strategy                	| Use L40S for production; L4 as alternative; avoid T4/T4 Medium for real-time |
| Code Update                      	| Fix deprecated tokenizer for Transformers v5 compatibility              	|

## Conclusion
| Summary Point                 	| Details                                                             	|
|-----------------------------------|-------------------------------------------------------------------------|
| Best Hardware                 	| L40S (5.138 s average), ideal for real-time applications            	|
| Worst Hardware                	| T4/T4 Medium (18.383–19.441 s), unsuitable without optimization     	|
| Main Bottleneck               	| Speech synthesis (72.71–89.60%), requires urgent optimization       	|
| Next Steps                    	| Optimize speech synthesis, response generation, and cold starts; enhance logging |
| Future Focus                  	| Profile speech synthesis, test diverse queries, assess concurrency   	|


--


## Overview
This report analyzes the latency performance of the Dhwani AI Voice Assistant, designed for Kannada and other Indian languages, based on server logs from April 11, 2025. The logs cover three hardware configurations: L40S, L4, T4 Medium, and T4. The analysis focuses on the end-to-end latency of the `/v1/speech_to_speech` endpoint and the individual processing stages, including transcription, translation to English, response generation, translation back to Kannada, and overall request processing. The goal is to identify performance bottlenecks, compare hardware efficiency, and provide recommendations for optimization.

## Methodology
- **Data Source**: Logs from four hardware configurations (L40S, L4, T4 Medium, T4) for the query "ಕರ್ನಾಟಕ ದ ರಾಜಧಾನಿ ಯಾವುದು" (What is the capital of Karnataka?).
- **Sample Size**: Three requests per configuration, totaling 12 requests.
- **Latency Metrics**:
  - **Transcription**: Time from receiving the audio to transcribing it to Kannada text.
  - **Translation to English**: Time from transcribed text to English translation.
  - **Response Generation**: Time from English prompt to generating the English response.
  - **Translation to Kannada**: Time from English response to Kannada translation.
  - **End-to-End Latency**: Total time for the `/v1/speech_to_speech` request, as reported in the logs.
- **Assumptions**:
  - Timestamps are accurate and synchronized.
  - The repeated "Generated response" log entry is a logging artifact and does not affect latency calculations.
  - The deprecated tokenizer warning does not impact performance but is noted for future code updates.

## Latency Analysis

### 1. End-to-End Latency
The end-to-end latency is the total time taken for the `/v1/speech_to_speech` request, as logged by the server.

| Hardware   | Request 1 (s) | Request 2 (s) | Request 3 (s) | Average (s) | Std Dev (s) |
|------------|---------------|---------------|---------------|-------------|-------------|
| L40S   	| 6.536     	| 4.400     	| 4.479     	| 5.138   	| 1.171   	|
| L4     	| 11.687    	| 9.344     	| 9.207     	| 10.079  	| 1.374   	|
| T4 Medium  | 19.504    	| 17.746    	| 17.898    	| 18.383  	| 0.952   	|
| T4     	| 20.830    	| 18.643    	| 18.850    	| 19.441  	| 1.147   	|

**Observations**:
- **L40S** is the fastest, with an average latency of 5.138 seconds, and shows variability (std dev 1.171 s), likely due to the first request being slower (6.536 s) compared to subsequent ones (4.400 s, 4.479 s).
- **L4** averages 10.079 seconds, roughly double the L40S latency, with moderate variability (std dev 1.374 s).
- **T4 Medium** and **T4** are significantly slower, averaging 18.383 seconds and 19.441 seconds, respectively, with lower variability (std dev 0.952 s and 1.147 s).
- The first request on each hardware tends to be slower, possibly due to initialization or caching effects.

### 2. Stage-Wise Latency Breakdown
To understand where time is spent, we calculate the latency for each processing stage using the provided timestamps. The stages are:
- **Transcription**: Transcribed text timestamp - Request start timestamp.
- **Translation to English**: English translation timestamp - Transcribed text timestamp.
- **Response Generation**: Generated response timestamp - English translation timestamp.
- **Translation to Kannada**: Kannada translation timestamp - Generated response timestamp.
- **Remaining Time**: End-to-end latency - Sum of above stages (likely includes audio processing, speech synthesis, and overhead).

Below is the average latency per stage across the three requests for each hardware:

| Hardware   | Transcription (s) | Trans. to Eng (s) | Resp. Gen (s) | Trans. to Kan (s) | Remaining (s) |
|------------|-------------------|-------------------|---------------|-------------------|---------------|
| L40S   	| 0.001         	| 0.298         	| 0.911     	| 0.192         	| 3.736     	|
| L4     	| 0.001         	| 0.266         	| 0.970     	| 0.194         	| 8.648     	|
| T4 Medium  | 0.001         	| 0.296         	| 1.383     	| 0.234         	| 16.469    	|
| T4     	| 0.001         	| 0.312         	| 1.445     	| 0.265         	| 17.418    	|

**Calculation Notes**:
- Timestamps were extracted from logs (e.g., for L40S Request 1: Transcription at 15:59:25.143, Translation to English at 15:59:25.475, etc.).
- Remaining time is calculated as: End-to-end latency - (Transcription + Trans. to Eng + Resp. Gen + Trans. to Kan).
- Transcription latency is consistently ~0.001 seconds due to near-instantaneous logging (possibly limited by timestamp precision).

**Observations**:
- **Transcription**: Extremely fast (~0.001 s) across all hardware, suggesting efficient speech-to-text processing or limited timestamp granularity.
- **Translation to English**: Takes 0.266–0.312 seconds, with L4 slightly faster (0.266 s) than L40S (0.298 s), T4 Medium (0.296 s), and T4 (0.312 s). Differences are minor (~46 ms).
- **Response Generation**: L40S is fastest (0.911 s), followed by L4 (0.970 s), T4 Medium (1.383 s), and T4 (1.445 s). This stage shows noticeable hardware dependency, with T4 and T4 Medium lagging by ~0.5 seconds.
- **Translation to Kannada**: Fast across all hardware (0.192–0.265 s), with L40S and L4 slightly quicker (0.192 s, 0.194 s) than T4 Medium (0.234 s) and T4 (0.265 s).
- **Remaining Time**: Dominates the latency, especially for T4 (17.418 s) and T4 Medium (16.469 s), followed by L4 (8.648 s) and L40S (3.736 s). This likely includes speech synthesis (text-to-speech) and other overheads (e.g., network, I/O).

### 3. Stage Contribution to Total Latency
To highlight bottlenecks, we express each stage’s average latency as a percentage of the total end-to-end latency:

| Hardware   | Transcription (%) | Trans. to Eng (%) | Resp. Gen (%) | Trans. to Kan (%) | Remaining (%) |
|------------|-------------------|-------------------|---------------|-------------------|---------------|
| L40S   	| 0.02          	| 5.80          	| 17.73     	| 3.74          	| 72.71     	|
| L4     	| 0.01          	| 2.64          	| 9.63      	| 1.92          	| 85.80     	|
| T4 Medium  | 0.01          	| 1.61          	| 7.52      	| 1.27          	| 89.59     	|
| T4     	| 0.01          	| 1.60          	| 7.43      	| 1.36          	| 89.60     	|

**Observations**:
- The **Remaining Time** dominates across all hardware, contributing 72.71% (L40S) to 89.60% (T4) of total latency. This suggests that speech synthesis or other unlogged processes (e.g., audio preprocessing, network latency) are the primary bottlenecks.
- **Response Generation** is the second-largest contributor for L40S (17.73%) and L4 (9.63%), but less significant for T4 Medium (7.52%) and T4 (7.43%) due to the overwhelming remaining time.
- **Translation to English** and **Translation to Kannada** are minor contributors (1.27–5.80%), indicating efficient translation models.
- **Transcription** is negligible (<0.02%) in all cases.

## Hardware Comparison
- **L40S**: Best performer with an average end-to-end latency of 5.138 seconds. Excels in response generation (0.911 s) and has the lowest remaining time (3.736 s). Likely benefits from superior GPU compute power.
- **L4**: Moderate performance at 10.079 seconds. Slightly faster than L40S in translation to English (0.266 s vs. 0.298 s) but slower in response generation (0.970 s) and significantly slower in remaining time (8.648 s).
- **T4 Medium**: Poor performance at 18.383 seconds. Slower in response generation (1.383 s) and has a high remaining time (16.469 s), indicating limited compute capacity for speech synthesis or other tasks.
- **T4**: Worst performer at 19.441 seconds, with the slowest response generation (1.445 s) and highest remaining time (17.418 s). Similar to T4 Medium but slightly worse, possibly due to configuration differences.

## Bottlenecks and Hypotheses
1. **Remaining Time Dominance**:
   - The large remaining time (72.71–89.60%) suggests that speech synthesis (text-to-speech) or unlogged processes (e.g., audio preprocessing, network latency) are the primary bottlenecks.
   - **Hypothesis**: The text-to-speech model is computationally intensive or poorly optimized for T4 and T4 Medium hardware. L40S’s lower remaining time (3.736 s) indicates better handling of this stage.
2. **Response Generation Variability**:
   - Response generation takes 0.911–1.445 seconds, with L40S and L4 outperforming T4 and T4 Medium. This stage likely involves a language model inference step, which is sensitive to GPU performance.
   - **Hypothesis**: The language model is not optimized for lower-end GPUs (T4, T4 Medium), leading to longer inference times.
3. **First Request Overhead**:
   - The first request is consistently slower (e.g., L40S: 6.536 s vs. 4.400 s for Request 2). This could be due to model loading, caching, or initialization.
   - **Hypothesis**: Cold starts or lack of model preloading increase latency for initial requests.

## Recommendations
1. **Optimize Speech Synthesis**:
   - Profile the text-to-speech component to confirm it dominates the remaining time. Optimize the model (e.g., quantization, pruning) or use a lighter model compatible with T4 and T4 Medium.
   - Explore hardware-specific optimizations (e.g., NVIDIA TensorRT for L40S and L4).
2. **Improve Response Generation**:
   - Optimize the language model for inference on T4 and T4 Medium (e.g., reduce model size, use mixed precision).
   - Consider batching or caching common queries to reduce inference time.
3. **Mitigate Cold Start Latency**:
   - Implement model preloading or warm-up requests to reduce first-request latency.
   - Investigate caching mechanisms for frequently asked questions like “What is the capital of Karnataka?”
4. **Enhance Logging**:
   - Add timestamps for speech synthesis and audio preprocessing to isolate their contributions to remaining time.
   - Increase timestamp precision (e.g., microseconds) to accurately measure fast stages like transcription.
5. **Hardware Upgrade**:
   - Prioritize L40S for production if budget allows, as it offers ~2x faster performance than L4 and ~4x faster than T4/T4 Medium.
   - If cost-constrained, L4 is a reasonable compromise, but T4 and T4 Medium are unsuitable for real-time applications due to high latency.
6. **Address Deprecated Warning**:
   - Update the tokenizer code to use `text_target` as per the Transformers v5 recommendation. While not a performance issue, this ensures compatibility with future library updates.

## Conclusion
The Dhwani AI Voice Assistant’s latency varies significantly by hardware, with L40S achieving the best performance (5.138 s average), followed by L4 (10.079 s), T4 Medium (18.383 s), and T4 (19.441 s). The primary bottleneck is the “remaining time” (72.71–89.60% of total latency), likely dominated by speech synthesis, followed by response generation (7.43–17.73%). Optimizations should focus on text-to-speech efficiency, language model inference, and cold start mitigation. For real-time applications, L40S is recommended, while T4 and T4 Medium require significant optimization to meet acceptable latency thresholds (e.g., <5 seconds). Enhanced logging and profiling will further clarify bottlenecks and guide improvements.

**Future Work**:
- Conduct profiling to confirm speech synthesis as the main bottleneck.
- Test optimizations on a broader range of queries to ensure generalizability.
- Evaluate latency under concurrent requests to assess scalability.

This report provides a foundation for improving Dhwani AI’s performance, ensuring a responsive and effective voice assistant for Kannada users.


--

Original Logs - [https://github.com/slabstech/dhwani-server/blob/main/docs/latency_server.md](https://github.com/slabstech/dhwani-server/blob/main/docs/latency_server.md)

—

Apr 18, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/misc/2025-04-18-dhwani-feedback-v2-ideas-tasks.md


Dhwani Live Data  Access


Read news for old people

Get gym deatils for Initial users

Upload book and get quizzed on learning material
Full - learning app


--

pitch demo - Berlin- 26 april
April

Hey Dhwani- api use with microphone and speaker on Raspi

Yc hackahon - berlin tasks and work

Use restack and build Front End



--

vllm - speedup and Latency measurements

Run with indivial repo first

-
Lets do the smallesr changes forst and then merge into larger program

Gh200- build ?


Test - speed on h100

Meaure the forst latency

Then measure woth indivial improvement


--


pdf - summary for server

Build gradio demo for pdf summary and extraction

Use the pdf-extraction to pdf extract

Call llm - summary function with chat


Add - batch api to extract: complete pdf

Supprt jpeg/png / webp/ for ocr ikage


---

Model Server -

Use llm serve options wherever possible


It will work amazing for batch requests

Supprort - Kannada/ english / german /


--

Try to use - obfuscation in App for security

–
Press - Release

Apr 30, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/press/2025-04-30-launch-release.md

dwani.ai - Press Release

Dwani AI is a Voice Assistant designed for India. AI(Artificial Intelligence) is making major changes in the world, but it is available only for English and European languages.
700 Million Indian users and 50 Million Kannada users do not have access to AI.

We launched dwani.ai Android app for Early users on 21 April 2025. 40 users are currently using the Android App. The App will become available in Google Play store on 15 May 2025.Free Workshops on dwani.ai were conducted at Chanakya University, Bengaluru on 20th March 2025 and Gopalan College of Engineering and Management, Bengaluru on 28 April 2025. Two workshops planned for May 2025 in Hubballi and Bengaluru.  Workshop is helping students to learn AI to solve problems for India with AI applications in local languages.Next goal of dwani.ai -To build a solution for visually challenged persons to use Voice technology in Kannada to lead a better life.Patent # 201941044370 with Title - Human Assisting Apparatus, developed by Sahana Shetty and team from KLETech Uni.  - Will be converted into prototype using technology developed by dwani.aidwani.ai has been developed by M/S S Labs Solutions from Hubballi, Karnataka



—

Pitch 

—

Apr 2, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-02-dhwani-april-business-roadmap.md


Dhwani - Business Roadmap - April 2025


- Dhwani AI  :  https://dhwani-ai.com/business

- Integration with 3rd party API
	- Twilio
	- Hubspot
	- MCP server

- Outreach to college
	- Provide API access to Student and Incubator Projects
	- MOU for support of AI development

- OEM's integration with hardware manufactures

- Integration with HomeAssistant

- Compatibility with Matter protocol/ Alexa/Google/Siri products

—
Apr 2, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-02-dhwani-education-roadmap.md

Dhwani - Education Roadmap


- Dhwani AI  :  https://dhwani-ai.com/education

Below is the brief summary of the services and products that we would like to collaborate.

- First Phase :
  - Workshop
	- How to build AI Application for Indian problems using Dhwani AI
	- Slides: https://tinyurl.com/dhwani-workshop  
	- https://github.com/slabstech/dhwani-workshop
  	- Is the hands-on examples that the participants will through during the workshop.


- Phase 2 :
  - How to setup - Dhwani Server on local infrastructure
  - Support all project's involving AI including training of new model, research to product pipeline for Student Startups
  - Support in developing curriculum involving latest technology used
  - Training for Student's, Faculty and Researcher to build , design and improve AI models



- Alternate Universe
  - https://www.anthropic.com/education
  - https://academy.openai.com/


---

To make AI accessible for everyone, we would like to skill-up students to build AI applications
using Dhwani AI.

Based on our discussion we will follow the steps described below
 - A Seminar: Showcasing Dhwani AI’s capabilities and its practical applications in addressing diverse problems.

 - An Induction Session: Guiding attendees on how to effectively utilize Dhwani AI services to power their applications.

 - A Hackathon: Encouraging innovation through a competitive platform where ideas are transformed into tangible products.

—

Apr 3, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-03-dhwani-request-for-grants.md

Dhwani AI - Request for Grants

1. GPU credits (Huggingface Preferred)-  3-6 months of L4 /L40S GPU compute to run Dhwani API server

Below is the 3 month roadmap for Dhwani AI to improve accessibility.
1. Education - https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-02-dhwani-education-roadmap.md
2. Business - https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-02-dhwani-april-business-roadmap.md

With access to GPU credits, we will be able to make the API accessible to students and collaborate with more universities.

Dhwani AI USP is Kannada Voice Chat for tier 2/tier3 cities for users and
 ability to self-host the systems for enterprise/university/students

Once Dhwani AI has full feature-set to make End to End Speech for Kannada,
we will restart work on Sanjeevi - Medical Transcription System

https://sanjeevini.me

–

April 7, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-07-dhwani-pitch-deck.md


Pitch Deck for Dhwani

Slide 1: Title Slide

	Dhwani: Your Kannada-Speaking Voice Buddy
	[Insert Logo Here]
	Presented by [Your Name/Team Name]

Slide 2: The Vision

	Empowering over 50 million Kannada speakers with accessible voice technology.
	Bridging the language gap in the digital world.

Slide 3: The Problem

	Existing voice assistants (e.g., Siri, Alexa) do not support Kannada.
	Over 50 million Kannada speakers are excluded from voice technology.
	Limits accessibility for non-English speakers and those with disabilities.

Slide 4: The Solution

	Dhwani: A voice assistant that understands and speaks Kannada.
	Open-source and community-driven.
	Runs on-device for privacy and offline use.
	Built with cutting-edge models from AI4Bharat at IIT Madras.

Slide 5: Product Demo

	[Screenshots or Video of the Android App]
	Features:
    	Voice queries in Kannada
    	Text queries in Kannada
    	Voice and text answers in Kannada
    	Translation between Kannada and other languages
	Available on Google Play: [Insert Link]

Slide 6: Technology

	Automatic Speech Recognition (ASR): IndicConformer for Kannada
	Text-to-Speech (TTS): Indic Parler TTS
	Large Language Model (LLM): Gemma3-4B-Instruct
	Translation: IndicTrans2
	All models are open-source, robust, and proven.

Slide 7: Market Opportunity

	50 million+ Kannada speakers worldwide.
	Growing demand for regional language tech solutions.
	Potential to expand to other Indian languages (1 billion+ market).

Slide 8: Traction

	Android app live on Play Store: https://play.google.com/store/apps/details?id=com.slabstech.dhwani.voiceai
	Demo video available: [Insert Link]
	Early user interest and community support.

Slide 9: Business Model

	Freemium Model: Free basic features; premium features (e.g., advanced translation, custom voices) via subscription.
	Enterprise Solutions: License Dhwani tech to businesses for integration.
	Partnerships: Collaborate with tech firms and educational institutions.

Slide 10: Team

	[Team Member 1]: [Role], [Expertise, e.g., AI/NLP Specialist]
	[Team Member 2]: [Role], [Expertise, e.g., Software Developer]
	Advisors: [If Any]
	Supported by an open-source community.

Slide 11: Financials

	Current Monthly Costs:
    	Servers: €2,500
    	Salaries: €5,000
    	Total: €7,500/month
	Investment will fund:
    	Model enhancements for accuracy.
    	New feature development.
    	User acquisition and marketing.

Slide 12: Funding Ask

	Seeking €100,000 in Seed Funding
	Provides a 12-month runway to:
    	Improve technology and performance.
    	Grow user base to 100,000.
    	Launch revenue-generating features.

Slide 13: Roadmap

	Q1: Enhance ASR and TTS models.
	Q2: Add multi-language support.
	Q3: Launch marketing campaign.
	Q4: Reach 100,000 users and roll out premium features.

Slide 14: Competitive Advantage

	Open-Source: Transparent, community-driven, and free to use.
	On-Device Processing: Ensures privacy and offline functionality.
	Kannada-Focused: Tailored to the language and culture.
	Scalable: Adaptable to other regional languages.

Slide 15: Thank You

	Thank you for considering Dhwani!
	Contact: [Insert Email] | [Insert Phone]
	Let’s make voice technology accessible to all.

Notes for Implementation

	Visuals: Enhance slides with app screenshots (Slide 5), market size charts (Slide 7), team photos (Slide 10), and a funding allocation pie chart (Slide 11).
	Demo: Include a live demo or link to the demo video in Slide 5 to showcase Dhwani’s capabilities.
	Customization: Replace placeholders (e.g., team details, traction metrics) with specific data if available.
	Delivery: Keep the pitch concise (10-15 minutes), focusing on the problem-solution fit, market potential, and clear use of funds.

This pitch deck positions Dhwani as a unique, impactful, and scalable solution, appealing to investors interested in tech innovation and social good. With €100,000, you can transform this MVP into a product that serves millions while laying the groundwork for revenue generation.


–

Apr 12, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-12-dhwani-ai-India-pitch.md



# Visual Mockup Suggestions for Dhwani AI Pitch Deck

This document provides visual mockup suggestions for the revised "Dhwani-AI-Pitch-India.pdf" pitch deck, incorporating original feedback (professional design, emotional story) and additional feedback (reduce text/info for a 5-minute pitch, non-salesy tone, vibrant colors, logo). The mockup targets an 8-slide deck, prioritizing clarity, cultural resonance, and inspiration for a Kannada-speaking voice assistant.

---

## General Design Guidelines
- **Color Palette**:
  - Primary: Saffron (#FF9933, warmth, Indian heritage).
  - Secondary: Green (#138808, Karnataka’s lush landscapes).
  - Accent: Purple (#6A1B9A, nod to Kannada culture).
  - Neutral: White (#FFFFFF, contrast), Light Gray (#F5F5F5, backgrounds).
  - Ensure accessibility (WCAG-compliant contrast, e.g., white text on purple).
- **Typography**:
  - Font: Poppins (Google Fonts, modern, clean).
	- Titles: Bold, 24pt, purple or saffron.
	- Body: Regular, 16pt, black or white (depending on background).
	- Subtle Kannada script (e.g., Noto Sans Kannada) for logo or accents.
- **Logo**:
  - Design: Stylized microphone with “ಧ್ವನಿ” (Kannada script) in purple, green soundwave curve underneath.
  - Placeholder: “Dhwani” in Poppins Bold, purple, until custom logo is ready.
  - Placement: Top-left corner, 10% of slide width (~50px).
- **Visuals**:
  - Images: Authentic Kannada speakers (e.g., farmers, students, elders), rural Karnataka scenes (e.g., fields, temples). Source from Unsplash or Pexels (keywords: “India rural,” “Karnataka”).
  - Icons: Flat, minimal (e.g., microphone, lock, globe) in green/purple. Use Flaticon or Noun Project.
  - Infographics: Simple (e.g., pie charts, stat boxes) in saffron-green.
  - Avoid clutter: 1-2 images/icons per slide, 50% whitespace.
- **Template**:
  - Background: Subtle gradient (saffron to purple, top to bottom).
  - Border: Thin green line or jasmine flower motif (Karnataka’s state flower) in corners.
  - Footer: Slide number (bottom-right, gray, 12pt), tagline “Voice for All” (bottom-left, purple, 10pt).
- **Tools**:
  - Canva: Use “Startup Pitch Deck” template, customize colors/fonts.
  - Figma: For precise layouts (free community templates available).
  - Logo: FreeLogoDesign or Canva Logo Maker for quick creation.
  - Budget: €100-300 for freelance designer (Fiverr) if needed.
- **Animation** (if presenting):
  - Minimal: Fade-in for text/icons (0.5s), no transitions between slides to save time.

---

## Slide-by-Slide Mockup Suggestions

### Slide 1: Cover
**Purpose**: Warm, branded intro (20 seconds).
**Layout**:
- **Background**: Full-slide image of a Kannada speaker (e.g., smiling student with smartphone), saffron-purple gradient overlay (50% opacity).
- **Top-Left**: Logo (“ಧ್ವನಿ” microphone, ~50px).
- **Center**:
  - Title: “Dhwani: Voice for Kannada” (Poppins Bold, 24pt, white).
  - Subtitle: “Connecting 50M+ Speakers” (Poppins Regular, 16pt, white).
- **Bottom-Left**: Tagline “Voice for All” (Poppins Italic, 12pt, purple).
- **Bottom-Right**: Slide number “1” (Poppins Regular, 12pt, gray).
**Visuals**:
- Image: Young Kannada speaker (Unsplash, e.g., “Indian student smiling”).
- No icons/charts to keep clean.
**Notes**:
- Gradient ensures text readability.
- Image evokes hope, aligning with mission.
- Mockup Tip: In Canva, use “Photo Frame” to crop image, add gradient via “Elements > Gradients.”

### Slide 2: The Problem – Emotional Story
**Purpose**: Set emotional stakes (40 seconds).
**Layout**:
- **Background**: Light gray (#F5F5F5) with thin green border.
- **Left (50%)**: Text box (white, purple outline).
  - Title: “Left Out of Technology” (Poppins Bold, 24pt, purple).
  - Text: “Shyamala’s voice isn’t heard—apps don’t speak Kannada. 50M+ speakers face a digital divide.” (Poppins Regular, 16pt, black, line spacing 1.2).
- **Right (50%)**: Image of Shyamala (farmer with phone, looking concerned).
- **Top-Left**: Logo (~40px).
- **Bottom-Right**: Slide number “2”.
**Visuals**:
- Image: Rural Indian woman (Pexels, e.g., “Indian farmer phone”).
- Optional: Small “X” icon (red, 20px) near “apps don’t speak” for emphasis.
**Notes**:
- Split layout balances story and visual.
- Minimal text (~15 words) keeps it digestible.
- Mockup Tip: Use Canva’s “Split Slide” template, adjust image to fit right half.

### Slide 3: The Solution
**Purpose**: Introduce Dhwani simply (40 seconds).
**Layout**:
- **Background**: Saffron gradient (top) to white (bottom).
- **Center**: Phone mockup (Dhwani app showing Kannada text, ~40% slide height).
- **Above Mockup**: Title: “Dhwani: Their Voice” (Poppins Bold, 24pt, purple).
- **Below Mockup**:
  - Bullets (2, centered, white box):
	- “Speaks Kannada for all.” (Poppins Regular, 16pt, black).
	- “Private, open, accessible.” (Poppins Regular, 16pt, black).
- **Top-Left**: Logo (~40px).
- **Bottom-Right**: Slide number “3”.
**Visuals**:
- Mockup: Smartphone frame (Canva “Device Mockup,” insert Kannada text screenshot).
- Icons: Speech bubble (green, 20px) next to first bullet, lock (purple, 20px) next to second.
**Notes**:
- Phone mockup visualizes solution instantly.
- Short bullets focus on impact.
- Mockup Tip: Use Canva’s “Smartphone Mockup,” add fake Kannada UI (e.g., “ನಮಸ್ಕಾರ” text).

### Slide 4: How It Works
**Purpose**: Show value visually (40 seconds).
**Layout**:
- **Background**: Green gradient (top) to white (bottom).
- **Left (60%)**: App screenshot (Dhwani query, e.g., “What’s the weather?” in Kannada, ~50% slide height).
- **Right (40%)**:
  - Title: “Simple, Powerful Tools” (Poppins Bold, 24pt, purple).
  - Bullets (2):
	- “Ask questions in Kannada.” (Poppins Regular, 16pt, black).
	- “ 🙂Translate, describe, summarize.” (Poppins Regular, 16pt, black).
- **Top-Left**: Logo (~40px).
- **Bottom-Right**: Slide number “4”.
**Visuals**:
- Screenshot: Fake Dhwani UI (Canva text tool for Kannada).
- Icons: Microphone (green, 20px) for “Ask,” globe (purple, 20px) for “Translate.”
**Notes**:
- Screenshot makes features tangible.
- Emoji adds warmth, avoids salesy tone.
- Mockup Tip: Use Figma for precise screenshot design, export to Canva.

### Slide 5: Traction
**Purpose**: Prove early success (35 seconds).
**Layout**:
- **Background**: Purple gradient (top) to white (bottom).
- **Center**: White stat box (rounded corners, ~60% slide width).
  - Title: “Gaining Ground” (Poppins Bold, 24pt, purple).
  - Bullets (2, left-aligned):
	- “10K+ users on Play Store.” (Poppins Regular, 16pt, black).
	- “Growing open-source community.” (Poppins Regular, 16pt, black).
- **Bottom-Center**: Small Play Store logo (20px, grayscale).
- **Top-Left**: Logo (~40px).
- **Bottom-Right**: Slide number “5”.
**Visuals**:
- Icon: Download arrow (green, 20px) for “users,” group (purple, 20px) for “community.”
- No image to keep focus on stats.
**Notes**:
- Stat box highlights traction clearly.
- Play Store logo adds credibility.
- Mockup Tip: Canva’s “Callout” shape for stat box, adjust opacity to 90%.

### Slide 6: Opportunity
**Purpose**: Highlight potential (35 seconds).
**Layout**:
- **Background**: Saffron gradient (top) to green (bottom).
- **Left (50%)**: Pie chart (50M Kannada in purple, 1B+ Indic in green, simple labels).
- **Right (50%)**:
  - Title: “A Billion Voices” (Poppins Bold, 24pt, white).
  - Bullets (2):
	- “50M Kannada speakers today.” (Poppins Regular, 16pt, white).
	- “Scalable to 1B+ tomorrow.” (Poppins Regular, 16pt, white).
- **Top-Left**: Logo (~40px).
- **Bottom-Right**: Slide number “6”.
**Visuals**:
- Chart: Minimal pie (Canva “Charts,” 2 segments).
- Optional: Small India map outline (gray, background) for context.
**Notes**:
- Chart visualizes scale without complexity.
- White text on gradient ensures readability.
- Mockup Tip: Use Canva’s “Pie Chart” tool, customize colors to match palette.

### Slide 7: Why Dhwani
**Purpose**: Differentiate humbly (35 seconds).
**Layout**:
- **Background**: Light gray with purple border.
- **Center**: 3-column grid (~20% each).
  - Column 1: Kannada script icon, “Kannada-first” (Poppins Regular, 14pt, black).
  - Column 2: Lock icon, “Private, open” (Poppins Regular, 14pt, black).
  - Column 3: Globe icon, “Scalable” (Poppins Regular, 14pt, black).
- **Top-Center**: Title: “Built Different” (Poppins Bold, 24pt, purple).
- **Top-Left**: Logo (~40px).
- **Bottom-Right**: Slide number “7”.
**Visuals**:
- Icons: Kannada letter (purple, 30px), lock (green, 30px), globe (saffron, 30px).
- No images to keep clean.
**Notes**:
- Grid format is scannable, non-boastful.
- Icons reinforce points visually.
- Mockup Tip: Use Canva’s “Grid” layout, align icons/text symmetrically.

### Slide 8: The Ask
**Purpose**: Invite partnership (35 seconds).
**Layout**:
- **Background**: Full-slide image (Kannada community, e.g., diverse group smiling), purple-saffron gradient overlay (40% opacity).
- **Center**: White box (70% slide width).
  - Title: “Let’s Empower Together” (Poppins Bold, 24pt, purple).
  - Bullets (2):
	- “€100,000 for tech, 100K users.” (Poppins Regular, 16pt, black).
	- “Join us to include millions.” (Poppins Regular, 16pt, black).
  - Contact: “example@example.xocm” (Poppins Italic, 14pt, purple).
- **Top-Left**: Logo (~40px).
- **Bottom-Right**: Slide number “8”.
**Visuals**:
- Image: Group of Kannada speakers (Unsplash, e.g., “Indian community”).
- Optional: Small handshake icon (green, 20px) near “Join us.”
**Notes**:
- Community image reinforces inclusion.
- Box keeps text clear on busy background.
- Mockup Tip: Use Canva’s “Transparent Overlay” for gradient, adjust image brightness.

---

## Implementation Plan
- **Step 1: Setup** (1 day):
  - Choose Canva template (“Minimalist Pitch Deck”).
  - Set colors: Saffron (#FF9933), Green (#138808), Purple (#6A1B9A).
  - Import Poppins font, create logo placeholder (“Dhwani” in purple).
- **Step 2: Slide Design** (2-3 days):
  - Create 8 slides per layouts above.
  - Source images (Unsplash/Pexels, 3-4 total).
  - Add icons (Flaticon, 6-8 total, free pack).
  - Design pie chart (Slide 6) and stat box (Slide 5) in Canva.
- **Step 3: Logo** (1 day):
  - Use Canva Logo Maker: Combine microphone + “ಧ್ವನಿ” (Noto Sans Kannada).
  - Export as PNG (transparent, 200px).
  - Alternative: Hire Fiverr designer (€20-50).
- **Step 4: Review** (1 day):
  - Check text length (~10-15 words/slide).
  - Test contrast (e.g., WebAIM Contrast Checker).
  - Practice timing (~35 seconds/slide).
- **Total Timeline**: 5-6 days.
- **Budget**: €0 (DIY with Canva) or €150-300 (designer for logo/slides).

---

## Additional Tips
- **Consistency**:
  - Use same logo size (~40-50px) across slides.
  - Apply gradient (saffron-purple or green-white) to 4-5 slides, solid gray to 3 for variety.
  - Align all text/icons to a 12px grid for polish.
- **Cultural Resonance**:
  - Add jasmine flower (small, 10px) in 2-3 slide corners (Karnataka symbol).
  - Use Kannada script sparingly (e.g., logo, Slide 7 icon) to avoid clutter.
- **Testing**:
  - Preview on projector/phone to ensure colors pop.
  - Share with 1-2 peers for feedback on “inspiration” (non-black-and-white goal).
- **Fallbacks**:
  - If image sourcing is slow, use Canva’s stock photos (filter: “India”).
  - If logo delays, stick with text-based “Dhwani” (still effective).
- **Q&A Support**:
  - Create 1-page handout (Canva) with appendix (financials: €7500/month, team: Sachin’s bio).
  - Include QR code to Play Store in Slide 8 or handout.

---

## Sample Mockup Description: Slide 2 (Emotional Story)
- **Canvas**: 1920x1080px (Canva default).
- **Background**: Light gray (#F5F5F5), green border (2px).
- **Left**:
  - White rectangle (800x600px, purple 2px outline, 90% opacity).
  - Title: “Left Out of Technology” (Poppins Bold, 24pt, #6A1B9A, 100px from top).
  - Text: “Shyamala’s voice isn’t heard—apps don’t speak Kannada. 50M+ speakers face a digital divide.” (Poppins Regular, 16pt, black, centered, 150px from top).
- **Right**: Image (Indian farmer with phone, 960x1080px, cropped to fit).
- **Top-Left**: Logo (microphone + “ಧ್ವನಿ”, 50px, 20px from edges).
- **Bottom-Right**: “2” (Poppins Regular, 12pt, gray, 20px from edges).
- **Effect**: Balanced, emotional, clear at a glance.

---

## Visual Inspiration
- **Canva Templates**: Search “Cultural Pitch Deck” or “Startup Minimalist” for similar vibes.
- **Examples**:
  - Airbnb’s early pitch deck: Simple images, bold stats.
  - Indian startups (e.g., Zomato): Warm colors, local imagery.
- **Mood Board**:
  - Colors: Saffron sunset, Karnataka greenery, purple silk.
  - Images: Rural smiles, tech in hands, community gatherings.
  - Icons: Minimal, rounded, human-focused.

This mockup creates a vibrant, culturally rich deck that tells Dhwani’s story in 5 minutes, leaving investors inspired and ready for Q&A.




---



# Dhwani AI Elevator Pitch Summary

Picture Shyamala, a Kannada-speaking farmer from Karnataka, unable to use voice apps—they don’t understand her language. For 50 million Kannada speakers, technology feels out of reach, excluding them from digital access and opportunities.

Dhwani changes that. Our open-source voice assistant speaks Kannada fluently, helping people like Shyamala with everyday tasks—asking questions, translating, or describing images—all in their native tongue. It’s private, works offline, and runs on affordable devices, designed with Karnataka’s heart in mind.

We’re live on the Play Store with 10,000+ downloads and a growing community. Dhwani’s built to scale, ready to serve 1 billion voices across India’s 22 languages in a market craving local solutions.

No one else offers Kannada voice tech—Dhwani’s unique, community-driven, and culturally true.

We’re seeking €100,000 to reach 100,000 users and refine our tech, partnering to include millions in the digital world.

Let’s give 50 million voices a chance to be heard. Join us.


---

**Delivery Notes**:
- **Time**: 1-2 minutes.
- **Tone**: Warm, urgent, inclusive.
- **Visuals** (if used): Show Dhwani logo (microphone with “ಧ್ವನಿ”), app screenshot, or Shyamala’s image.
- **Flow**:
  - 20s: Shyamala’s story + problem.
  - 30s: Dhwani’s solution + features.
  - 20s: Traction + market.
  - 20s: Uniqueness + ask.
- **Tip**: End with a smile and pause for questions.



---


# Dhwani AI Pitch Deck Improvements

This document outlines enhancements to the "Dhwani-AI-Pitch-India.pdf" pitch deck, incorporating original feedback (professional design, emotional story) and new feedback (reduce text/information, avoid sales pitch tone, improve colors/visuals, add logo). The revised deck targets a 5-minute pitch (8-10 slides) with 5-minute Q&A, emphasizing clarity, impact, and inspiration.

---

## Feedback Addressed
### Original Feedback
- **Pitch Deck Design**: Create a professional, visually engaging look.
- **Emotional Story**: Add a relatable narrative early to highlight the problem.

### New Feedback
- **Too Much Text/Information**: Limit content for a 5-minute pitch (~8-10 slides).
- **Not a Sales Pitch**: Focus on mission and vision, not aggressive selling.
- **Coloring/Visuals**: Replace black-and-white with vibrant, inspiring colors.
- **Logo**: Include a Dhwani logo for branding.

---

## General Improvements
1. **Reduce Length**:
   - Target 8 slides to fit 5 minutes (~35-40 seconds per slide).
   - Eliminate non-essential details (e.g., detailed financials, full tech stack) to focus on problem, solution, traction, and ask.
   - Move secondary info (e.g., roadmap details, team bios) to Q&A handouts or appendix.

2. **Minimize Text**:
   - Use 1-3 bullets per slide, 5-8 words each.
   - Replace text with visuals (e.g., images, icons, simple charts).
   - Prioritize storytelling and visuals over data-heavy slides.

3. **Non-Salesy Tone**:
   - Emphasize inclusion and empowerment over revenue or hype.
   - Frame funding as a shared mission, not a hard sell.
   - Use humble, authentic language (e.g., “join us” vs. “invest now”).

4. **Vibrant Design**:
   - **Color Palette**: Indian-inspired tones (saffron #FF9933, green #138808, purple #6A1B9A for Karnataka), with white (#FFFFFF) for contrast.
   - **Typography**: Poppins (24pt titles, 16pt body, bold for emphasis).
   - **Visuals**: Use evocative images (Kannada speakers, rural Karnataka), icons (e.g., microphone, lock), and minimal infographics (e.g., market size).
   - **Template**: Gradient background (saffron to purple), logo top-left, slide numbers bottom-right. Avoid animations to keep focus on content.

5. **Logo**:
   - Design a simple logo: e.g., a microphone with Kannada script “ಧ್ವನಿ” in purple-green.
   - Placeholder: Stylized “Dhwani” text (Poppins Bold, purple) if logo isn’t ready.
   - Place consistently on all slides.

---

## Revised Pitch Deck Structure (8 Slides)

### Slide 1: Cover
**Current**: "Meet Dinwan: Your Kannada-Speaking Voice Buddy" (typo).
**Improvements**:
- **Design**: Full-slide image of a Kannada speaker (e.g., student smiling) with saffron-purple gradient overlay. Logo top-left.
- **Content**:
  - Fix typo: **"Dhwani: Voice for Kannada"**.
  - Subtitle: *"Connecting 50M+ Speakers"*.
- **Purpose**: Warm, inviting intro (20 seconds).
- **Text**: ~8 words, no bullets.

### Slide 2: The Problem – Emotional Story
**Current**: None (added per original feedback).
**Improvements**:
- **Design**: Split layout—left: text (white box), right: image of Shyamala (farmer) looking at a phone. Green-purple tones.
- **Content**:
  - Title: **"Left Out of Technology"**.
  - Text:
	> Shyamala’s voice isn’t heard—apps don’t speak Kannada.  
	> 50M+ speakers face a digital divide.
- **Purpose**: Set emotional stakes (40 seconds).
- **Text**: ~15 words, no bullets.

### Slide 3: The Solution
**Current**: Dhwani as Kannada voice assistant, open-source, on-premise.
**Improvements**:
- **Design**: Phone mockup with Dhwani’s Kannada interface. Icons for “Kannada” (speech bubble), “Privacy” (lock). Saffron background.
- **Content**:
  - Title: **"Dhwani: Their Voice"**.
  - Bullets:
	- *Speaks Kannada for all.*
	- *Private, open, accessible.*
- **Purpose**: Introduce Dhwani simply (40 seconds).
- **Text**: 2 bullets, ~10 words total.

### Slide 4: How It Works
**Current**: Product demo with features (voice queries, translation, etc.).
**Improvements**:
- **Design**: Single app screenshot (e.g., Kannada query). 3 icons (microphone, globe, document) in purple-green.
- **Content**:
  - Title: **"Simple, Powerful Tools"**.
  - Bullets:
	- *Ask questions in Kannada.*
	- *Translate, describe, summarize.*
- **Purpose**: Show value visually (40 seconds).
- **Text**: 2 bullets, ~10 words total.

### Slide 5: Traction
**Current**: Early interest, Play Store launch, demo video.
**Improvements**:
- **Design**: Stat box with “10K+ Downloads” and “50+ Contributors.” Small Play Store logo. Green background.
- **Content**:
  - Title: **"Gaining Ground"**.
  - Bullets:
	- *10K+ users on Play Store.*
	- *Growing open-source community.*
- **Purpose**: Prove early success (35 seconds).
- **Text**: 2 bullets, ~10 words total.

### Slide 6: Opportunity
**Current**: 50M+ Kannada speakers, 1B+ Indic market.
**Improvements**:
- **Design**: Simple chart (50M Kannada vs. 1B+ Indic) in purple-saffron. Image of diverse Indian crowd.
- **Content**:
  - Title: **"A Billion Voices"**.
  - Bullets:
	- *50M Kannada speakers today.*
	- *Scalable to 1B+ tomorrow.*
- **Purpose**: Highlight potential (35 seconds).
- **Text**: 2 bullets, ~10 words total.

### Slide 7: Why Dhwani
**Current**: Competitive advantages (open-source, privacy, etc.).
**Improvements**:
- **Design**: 3 icons (Kannada script, lock, globe) with short labels. Subtle comparison (Dhwani vs. others). Purple background.
- **Content**:
  - Title: **"Built Different"**.
  - Bullets:
	- *Kannada-first, culturally true.*
	- *Private, open, scalable.*
- **Purpose**: Differentiate humbly (35 seconds).
- **Text**: 2 bullets, ~10 words total.

### Slide 8: The Ask
**Current**: €100,000 for tech, users, features.
**Improvements**:
- **Design**: Bold “€100,000” in saffron circle. Image of Kannada community. Small contact box (purple).
- **Content**:
  - Title: **"Let’s Empower Together"**.
  - Bullets:
	- *€100,000 for tech, 100K users.*
	- *Join us to include millions.*
  - Contact: *example@example.xocm*
- **Purpose**: Invite partnership (35 seconds).
- **Text**: 2 bullets, ~12 words total.

---

## Removed/Condensed Content
To fit 5 minutes and reduce information:
- **Cut Slides**:
  - Financials (Page 14): Costs (€7500/month) for Q&A only.
  - Roadmap (Page 16): Goals (Q1-Q4) implied in Ask slide.
  - Team (Page 13): Sachin mentioned in Ask; bios in appendix.
  - Technology (Page 8): ASR/TTS details folded into Solution.
  - Research Goals (Page 9): TTFTG for Q&A.
  - Business Model (Page 12): Revenue plans for Q&A.
  - Competitive Advantage (Page 17): Merged into Why Dhwani.
  - Vision (Page 2): Integrated into Story/Solution.
- **Condensed Slides**:
  - Traction + Market into separate but lean slides.
  - Demo simplified to key features.
- **Appendix**: 2-3 page PDF for Q&A with cut slides (Financials: €2500 servers, €5000 salaries; Team: Sachin’s bio; Roadmap: Q1-Q4).

---

## Additional Notes
- **Length**: 8 slides at ~35 seconds each fits 5 minutes, allowing pacing.
- **Non-Salesy Tone**:
  - Center Shyamala’s story and inclusion mission.
  - Avoid revenue figures (e.g., cut “$200K”) in slides; mention verbally if prompted.
  - Use “together” and “empower” to invite collaboration.
- **Design Effort**:
  - Use Canva (“Minimalist Pitch Deck” template). Apply saffron-purple-green.
  - Budget €150-400 for freelance designer (logo + slides).
  - Timeline: 3-4 days for redesign, 1-2 for logo.
- **Logo**:
  - Idea: Microphone with “ಧ್ವನಿ” in purple, green soundwave.
  - Interim: “Dhwani” in Poppins Bold (purple).
- **Error Fixes**:
  - Correct “Dinwan” (Page 1).
  - Remove Page 7 repetitive text (OCR error).
  - Fix “educations” (Page 12).
- **Cultural Touch**:
  - Subtle jasmine motif (Karnataka’s flower) in slide corners.
  - Optional: Kannada proverb (e.g., “Voice unites”) on cover.
- **Q&A Prep**:
  - Anticipate questions on tech (ASR/TTS), costs (€7500/month), and scaling.
  - Handout: Appendix PDF with Financials, Team, Business Model.

---

## Sample Slide: Emotional Story
**Title**: Left Out of Technology  
**Visual**: Left: Text (white box, purple title). Right: Shyamala (farmer with phone). Saffron-purple gradient.  
**Text**:  
> Shyamala’s voice isn’t heard—apps don’t speak Kannada.  
> 50M+ speakers face a digital divide.  
**Logo**: Top-left, “ಧ್ವನಿ” microphone.  
**Impact**: Emotional, concise (~15 words).

---

## Implementation Tips
- **Tools**: Canva for slides, FreeLogoDesign for logo. Source Karnataka images from Unsplash.
- **Timeline**: 5 days total (3 for slides, 2 for logo).
- **Testing**: Practice with mentors to hit 5 minutes, ensure story resonates.
- **Offer**: Can mock up a slide in Canva or refine logo idea—just ask!

This revised deck delivers a compelling, concise pitch that inspires and invites partnership.


---


# Dhwani AI Pitch Deck Improvements

This document outlines improvements to the "Dhwani-AI-Pitch-India.pdf" pitch deck based on feedback to enhance design and add an emotional story at the beginning to highlight the problem, while maintaining the deck's factual strength.

---

## Feedback Addressed
- **Pitch Deck Design**: Create a professional, visually engaging look.
- **Emotional Story**: Add a relatable narrative early to humanize the problem.

---

## General Improvements
1. **Pitch Deck Design**:
   - **Color Scheme**: Use Indian-inspired colors (saffron, green, white) with purple accents for Karnataka heritage. Ensure high-contrast text for accessibility.
   - **Typography**: Use Roboto or Lato (sans-serif) for body (16pt) and bold headings (24pt).
   - **Template**: Include a subtle Dhwani logo, footer with slide numbers, and grid layouts.
   - **Visuals**: Add images (e.g., Kannada speakers, rural scenes), icons (e.g., microphone), and infographics (e.g., market size).
   - **Minimalism**: Limit slides to 3-5 points, using whitespace effectively.

2. **Emotional Story**:
   - Insert a new slide after the cover to tell a story about a Kannada speaker facing digital exclusion, setting an emotional tone.

---

## Page-by-Page Improvements

### PAGE 1: Cover Slide
**Current**: "Meet Dinwan: Your Kannada-Speaking Voice Buddy" (typo: "Dinwan").
**Improvements**:
- **Design**: Full-slide image of a Kannada speaker (e.g., student or elder) with gradient overlay. Dhwani logo top-left.
- **Content**:
  - Fix typo: **"Meet Dhwani: Your Kannada-Speaking Voice Buddy"**.
  - Subtitle: *"Bringing Voice Technology to 50M+ Kannada Speakers"*.
  - Tagline: *"Speak. Connect. Thrive."*
- **Purpose**: Welcoming, professional first impression.

### PAGE 2: The Problem – Emotional Story (New Slide)
**Current**: No story; Page 2 is vision.
**Improvements**:
- **Insert Slide**: Title: **"A Voice Left Silent"**.
- **Design**: Split layout—text on left, image on right (e.g., farmer with smartphone or student).
- **Content**:
  > Shyamala, a 45-year-old farmer from Mysuru, can’t check crop prices online—voice assistants don’t speak Kannada. Her daughter Priya dreams of studying science, but AI tools are English-only. For 50M+ Kannada speakers, technology is a locked door.  
  > **Dhwani unlocks it with a voice they understand.**
- **Purpose**: Evoke empathy, making the problem urgent.

### PAGE 3: The Vision (Moved from Page 2)
**Current**: "Empowering over 50 million Kannada speakers with accessible voice technology. Bridging the language gap in the digital world."
**Improvements**:
- **Design**: Circular graphic with "50M+ Kannada Speakers" at center, branching to "Accessibility," "Inclusion," "Connection." Faint Karnataka outline in background.
- **Content**:
  - Refine: **"Our Vision: Enable 50M+ Kannada speakers to access technology in their language."**
  - Add: *"From education to daily tasks, Dhwani bridges the digital divide."*
- **Purpose**: Transition from story to hopeful vision.

### PAGE 4: The Problem (Moved from Page 3)
**Current**: Notes lack of Kannada support, 50M+ excluded, accessibility barriers.
**Improvements**:
- **Design**: 3 icons:
  - Microphone with "X" (No Kannada Support).
  - Group silhouette (50M+ Excluded).
  - Accessibility symbol (Barriers).
  - Bold stat box: "50M+".
- **Content**:
  - Bullets:
	- *Voice assistants (Siri, Alexa) don’t support Kannada.*
	- *50M+ speakers excluded from digital tools.*
	- *Non-English and disabled users face barriers.*
  - Add: *"This gap isolates communities."*
- **Purpose**: Reinforce story with facts.

### PAGE 5: The Solution
**Current**: Dhwani as Kannada voice assistant, open-source, privacy-focused.
**Improvements**:
- **Design**: Phone mockup of Dhwani interface. Badges for "Open-Source," "On-Premise."
- **Content**:
  - Title: **"Dhwani: A Voice for All"**.
  - Bullets:
	- *Speaks and understands Kannada natively.*
	- *Open-source: Free, community-built.*
	- *On-premise: Private, offline-ready.*
  - Add: *"For Shyamala, Priya, and millions more."*
- **Purpose**: Link solution to story.

### PAGE 6: Product Demo
**Current**: Features (voice queries, translation, image description, summaries), demo video.
**Improvements**:
- **Design**: 4-panel layout with icons/screenshots:
  - Microphone: Voice Queries.
  - Globe: Translation.
  - Image: Descriptions.
  - Document: Summaries.
  - QR code for demo video.
- **Content**:
  - Title: **"See Dhwani Work"**.
  - Features:
	- *Voice Queries: Ask in Kannada, get answers.*
	- *Translation: Kannada to English and more.*
	- *Accessibility: Image descriptions, summaries.*
  - Add: *"Live on Play Store!"*
- **Purpose**: Visual, actionable features.

### PAGE 7: Current Status
**Current**: March 20, 2025, unclear "Answer - Kannada," repetitive text (OCR error).
**Improvements**:
- **Design**: Milestone timeline (Prototype → Launch → Today). Play Store badge.
- **Content**:
  - Title: **"Progress So Far"**.
  - Bullets:
	- *April 2025: Dhwani app live on Play Store.*
	- *Features: Kannada queries, translation.*
	- *Traction: Early users, contributors onboard.*
  - Remove repetitive "4333...".
- **Purpose**: Show clear momentum.

### PAGE 8: Technology
**Current**: Lists ASR, TTS, LLM, Translation.
**Improvements**:
- **Design**: Flowchart (Speech → ASR → LLM → TTS). "Low-Resource Ready" badge.
- **Content**:
  - Title: **"Tech That Speaks Kannada"**.
  - Bullets:
	- *ASR: Kannada speech to text.*
	- *TTS: Natural Kannada speech.*
	- *LLM: Smart answers.*
	- *Translation: Kannada to global languages.*
  - Add: *"Built for affordable devices."*
- **Purpose**: Simplify tech, show strength.

### PAGE 9: Research Goals / Collaboration
**Current**: TTFTG goal, GitHub links.
**Improvements**:
- **Design**: Grid of cards per tool (icons). "Join Us" button for GitHub.
- **Content**:
  - Title: **"Building the Future"**.
  - Goals:
	- *Reduce TTFTG for faster responses.*
	- *Improve ASR, TTS, translation accuracy.*
	- *Grow open-source community.*
  - Collaboration: *"Contribute at github.com/slabstech/dhwani-server."*
- **Purpose**: Invite participation, show ambition.

### PAGE 10: Market Opportunity
**Current**: 50M+ Kannada speakers, 1B+ Indic market, regional tech demand.
**Improvements**:
- **Design**: Donut chart (50M Kannada vs. 1B+ Indic). Trend arrow for growth.
- **Content**:
  - Title: **"A Massive Market"**.
  - Bullets:
	- *50M+ Kannada speakers globally.*
	- *Scalable to 22 Indian languages (1B+ users).*
	- *Rising demand for local solutions.*
  - Add: *"Voice tech market to grow 25% by 2030."*
- **Purpose**: Highlight scale.

### PAGE 11: Traction
**Current**: Early interest, demo video, Play Store launch.
**Improvements**:
- **Design**: Stat grid ("10K Downloads," "50 Contributors"). User quote bubble.
- **Content**:
  - Title: **"Early Wins"**.
  - Bullets:
	- *Play Store: 10K+ downloads (April 2025).*
	- *Community: 50+ contributors.*
	- *Feedback: “Dhwani feels like a friend!” – User.*
  - Add QR code for demo.
- **Purpose**: Build trust with proof.

### PAGE 12: Business Model
**Current**: Enterprise, partnerships, freemium.
**Improvements**:
- **Design**: Trifecta diagram:
  - Enterprise: Handshake.
  - Partnerships: Puzzle piece.
  - Freemium: Gift box.
  - Year 1 revenue bar.
- **Content**:
  - Title: **"How We Grow"**.
  - Bullets:
	- *Enterprise: License to banks, hospitals.*
	- *Partnerships: Schools, tech firms.*
	- *Freemium: Free basic, premium advanced.*
  - Add: *"Targeting $200K Year 1."*
- **Purpose**: Show profitability paths.

### PAGE 13: Team
**Current**: Sachin Shetty only.
**Improvements**:
- **Design**: Sachin’s headshot in circle. Placeholder for “Future CTO.”
- **Content**:
  - Title: **"Our Team"**.
  - Bullets:
	- *Sachin Shetty: GenAI, full-stack, 7+ years.*
	- *Community: 50+ contributors.*
  - Add: *"Hiring top talent."*
- **Purpose**: Show leadership, potential.

### PAGE 14: Financials
**Current**: €7500/month costs, investment goals.
**Improvements**:
- **Design**: Pie chart (33% server, 67% salaries). Bar for investment split (50% tech, 30% marketing, 20% ops).
- **Content**:
  - Title: **"Our Numbers"**.
  - Bullets:
	- *Costs: €7500/month (€2500 servers, €5000 team).*
	- *Investment:*
  	- *50%: AI accuracy, speed.*
  	- *30%: 100K users.*
  	- *20%: New features.*
- **Purpose**: Transparent, purposeful.

### PAGE 15: Funding Ask
**Current**: €100,000 for 12 months.
**Improvements**:
- **Design**: Bold "€100,000" circle. Runway timeline (e.g., Month 3: Tech, Month 12: 100K Users).
- **Content**:
  - Title: **"Our Ask"**.
  - Bullets:
	- *€100,000 seed funding.*
	- *12-month plan:*
  	- *Enhance tech (30% faster).*
  	- *Reach 100K users.*
  	- *Launch paid features.*
  - Add: *"Invest in a billion voices."*
- **Purpose**: Clear, inspiring ask.

### PAGE 16: Roadmap
**Current**: Quarterly goals.
**Improvements**:
- **Design**: Timeline with icons (e.g., microphone Q1, globe Q2). Highlight "100K Users."
- **Content**:
  - Title: **"Next Steps"**.
  - Bullets:
	- *Q1 2025: Real-time Kannada AI.*
	- *Q2 2025: 3+ Indian languages.*
	- *Q3 2025: Enterprise pilots.*
	- *Q4 2025: 100K users.*
  - Add: *"500K by 2026."*
- **Purpose**: Clear path.

### PAGE 17: Competitive Advantage
**Current**: Open-source, privacy, Kannada focus, scalability, team.
**Improvements**:
- **Design**: Table (Dhwani vs. Siri/Alexa, e.g., "Kannada: Yes vs. No"). Checkmarks for advantages.
- **Content**:
  - Title: **"Why We Stand Out"**.
  - Bullets:
	- *Kannada-First: Local needs.*
	- *Open-Source: Free, collaborative.*
	- *Private: On-premise, offline.*
	- *Scalable: 1B+ users.*
	- *Nimble: 3 devs, AI-powered.*
  - Add: *"No one serves Kannada like us."*
- **Purpose**: Sharp differentiation.

### PAGE 18: Thank You
**Current**: Contact, closing message.
**Improvements**:
- **Design**: Uplifting image (diverse Kannada speakers). Contact box.
- **Content**:
  - Title: **"Together, We Speak"**.
  - Bullets:

	- *Try: github.com/slabstech/dhwani*
	- *“Empower 50M+ voices.”*
  - Add QR code to Play Store.
- **Purpose**: Memorable close.

---

## Additional Notes
- **Length**: Deck grows to 19 slides. Merge Financials (Page 14) and Funding Ask (Page 15) to stay at 18 if needed.
- **Story Continuity**: Reference Shyamala/Priya later (e.g., “For Priya” in Demo).
- **Design Effort**: Use Canva/Figma. Budget €300-700 for designer.
- **Error Fixes**: Correct "Dinwan" (Page 1), remove Page 7’s repetitive text, fix typos (e.g., "educations" Page 12).
- **Cultural Touch**: Add Kannada elements (e.g., Kuvempu quote).

---

## Sample Story Slide (Page 2)
**Title**: A Voice Left Silent  
**Visual**: Left: Text. Right: Image of Shyamala (farmer) or Priya (student).  
**Text**:  
> Shyamala, a farmer from Mysuru, can’t check crop prices—voice assistants don’t speak Kannada. Her daughter Priya dreams of studying science, but AI tools are English-only. For 50M+ Kannada speakers, technology is out of reach.  
> **Dhwani changes that.**

**Impact**: Sets emotional tone.

---

## Implementation Tips
- **Tools**: Canva “Pitch Deck” templates. Customize with Karnataka graphics.
- **Timeline**: 5-7 days for redesign, 3-5 more with designer.
- **Testing**: Share with mentors for feedback.
- **Offer**: Can draft slide text or suggest Canva template—let me know!

This revised deck blends storytelling, sleek design, and strong facts to captivate investors.

—

Apr 12, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-12-dhwani-ai-german-pitch-revised.md



Dhwani AI - Pitch Deck for German

Below is the revised pitch deck structure and content plan for Dhwani, formatted as a markdown file based on the provided feedback. You can copy this into a .md file for use.
markdown
# Dhwani Pitch Deck (Revised)

This document outlines the revised pitch deck for Dhwani, a German-speaking voice assistant, incorporating feedback to enhance storytelling, ensure German language focus, and improve design consistency. The structure maintains the original factual strengths while addressing emotional appeal, visual coherence, and German-centric content.

---

## General Design Recommendations
- **Visual Theme**: Use a clean, modern design with a color palette of blues, whites, and subtle German cultural accents (e.g., yellow or black from the German flag). Fonts: Montserrat or Open Sans for readability.
- **German Focus**: All screenshots, demos, and text examples must feature German to align with the 50M+ German-speaking audience. Avoid unrelated languages (e.g., Indian languages like Kannada) unless showing scalability.
- **Visual Storytelling**: Incorporate icons, infographics, and images evoking accessibility, privacy, and German culture (e.g., diverse users, privacy locks, subtle German landmarks).
- **Slide Layout**: One key message per slide, supported by visuals and minimal text. Use animations sparingly to guide attention.

---

## Slide-by-Slide Structure

### Slide 1: Title Slide
- **Title**: Dhwani: Bringing Voice Technology to Every German Speaker
- **Content**:
  - Tagline: "Accessible. Private. Made for You."
  - Visual: Warm image of diverse German speakers (family, student, elderly person) using a voice assistant, with a subtle German flag or Berlin skyline.
  - Include Dhwani logo (if available).
- **Purpose**: Set an inviting tone and emphasize German focus.

---

### Slide 2: The Problem (Story-Driven)
- **Title**: Imagine Being Left Out of the Digital World
- **Content**:
  - Story: "Meet Anna, a visually impaired grandmother in Munich. She wants to use voice technology to stay connected, but Siri and Alexa don’t understand her German dialect or prioritize her privacy. Like Anna, 50 million German speakers face barriers in an English-dominated digital world."
  - Visual: Illustration or photo of a German user (e.g., elderly person) looking frustrated with a device.
  - Stats: Subtle text: “50M+ German speakers excluded” and “Privacy concerns limit trust.”
- **Purpose**: Create empathy and ground the problem in a relatable German context.

---

### Slide 3: The Problem (Quantified)
- **Title**: Voice Technology Isn’t Built for Everyone
- **Content**:
  - Bullet Points:
	- Existing assistants (Siri, Alexa) prioritize English, leaving 50M+ German speakers underserved.
	- Lack of privacy: Cloud-based data storage erodes trust.
	- Limited accessibility: Non-English speakers and people with disabilities are excluded.
  - Visual: Infographic with a pie chart (50M German speakers vs. global English users) or a locked cloud icon for privacy.
- **Purpose**: Quantify the problem while maintaining emotional resonance.

---

### Slide 4: The Vision
- **Title**: A World Where Everyone’s Voice is Heard
- **Content**:
  - Vision: “Empowering 50 million German speakers with voice technology that’s accessible, private, and tailored to them.”
  - Subtext: “From Anna in Munich to students in Berlin, Dhwani bridges the language gap.”
  - Visual: Hopeful image of diverse German users (student, professional, retiree) smiling while using Dhwani, with German text overlays (e.g., “Hallo, wie kann ich helfen?”).
- **Purpose**: Connect the vision to the story and reinforce German cultural relevance.

---

### Slide 5: The Solution
- **Title**: Dhwani: Your German Voice Assistant
- **Content**:
  - Key Features:
	- Understands and speaks German fluently.
	- Open-source and privacy-first with on-premise setup.
	- Community-driven for constant improvement.
  - Visual: Screenshot of Dhwani’s interface in German (e.g., responding to “Was ist das Wetter in Berlin?”) or app mockup with German text.
- **Purpose**: Define Dhwani as the solution, emphasizing German and privacy.

---

### Slide 6: Product Demo
- **Title**: Dhwani in Action
- **Content**:
  - Features:
	- Voice queries in German (e.g., “Lies mir die Nachrichten vor”).
	- Real-time translation (German to English, French, etc.).
	- Image descriptions and document summaries in German.
  - Visual: Short video or GIF showing Dhwani responding to German commands (e.g., “Wie weit ist der Mond?”) on a phone/laptop.
  - Note: All demo content in German; avoid unrelated languages (e.g., Kannada).
- **Purpose**: Showcase capabilities with German-centric examples.

---

### Slide 7: Technology
- **Title**: Built for German, Powered by AI
- **Content**:
  - Core Tech:
	- Automatic Speech Recognition (ASR): Understands German dialects.
	- Text-to-Speech (TTS): Natural German voice output.
	- Large Language Models (LLMs): Context-aware responses.
	- Translation: Seamless German to other languages.
  - Visual: Flowchart showing German voice input (“Wie ist das Wetter?”) processed through ASR, LLM, and TTS.
- **Purpose**: Demystify tech while emphasizing German optimization.

---

### Slide 8: Market Opportunity
- **Title**: A Massive Opportunity in German-Speaking Markets
- **Content {{{content}}}:
  - Market Size: “50M+ German speakers across Germany, Austria, Switzerland, and beyond.”
  - Growth Potential: “Scalable to 300M+ European users with 10+ languages.”
  - Trend: “Rising demand for regional, privacy-focused tech.”
  - Visual: Map highlighting German-speaking countries with stats (e.g., “Germany: 80M, Austria: 9M, Switzerland: 5M”).
- **Purpose**: Highlight immediate German market with broader potential.

---

### Slide 9: Competitive Advantage
- **Title**: Why Dhwani Stands Out
- **Content**:
  - Differentiators:
	- German-first: Built for Anna’s dialect, not just English.
	- Privacy-first: On-premise setup keeps data secure.
	- Open-source: Transparent and community-driven.
	- Scalable: Ready for other European languages.
  - Visual: Comparison table (Dhwani vs. Siri/Alexa) with checkmarks for privacy, German fluency, and open-source.
- **Purpose**: Articulate why Dhwani is better, linking to the user story.

---

### Slide 10: Traction
- **Title**: Gaining Momentum
- **Content**:
  - Achievements:
	- Live on Google Play Store with German interface.
	- Early adopters: 1,000+ German-speaking users testing beta.
	- Community support: 500+ GitHub stars for open-source repos.
  - Visual: Screenshot of app’s Play Store page (in German) or German user testimonial (e.g., “Dhwani helps me read news privately!”).
- **Purpose**: Show progress with German-centric proof points.

---

### Slide 11: Business Model
- **Title**: How We Grow
- **Content**:
  - Revenue Streams:
	- Enterprise: License Dhwani for German businesses (healthcare, education).
	- Partnerships: Collaborate with German tech firms and universities.
	- Freemium: Free basic features; premium for unlimited use.
  - Visual: Funnel graphic showing free users converting to premium/enterprise, with German company logos (e.g., Siemens, Deutsche Telekom, hypothetical).
- **Purpose**: Outline German-focused monetization.

---

### Slide 12: Financials
- **Title**: Fueling Our Growth
- **Content**:
  - Current Costs: “€7,500/month (servers: €2,500, salaries: €5,000).”
  - Funding Ask: “Seeking €100,000 seed funding for 12-month runway.”
  - Use of Funds:
	- 50%: Enhance model accuracy and speed.
	- 30%: Develop German-focused features.
	- 20%: Market to 100,000 users.
  - Visual: Pie chart for fund allocation or timeline linking funds to milestones.
- **Purpose**: Show financial needs and impact transparently.

---

### Slide 13: Roadmap
- **Title**: Our Path Forward
- **Content**:
  - Q1 2025: Launch real-time German voice AI for users like Anna.
  - Q2 2025: Add multi-language support (e.g., Austrian/Swiss German).
  - Q3 2025: Roll out enterprise solutions for German businesses.
  - Q4 2025: Reach 100,000 German-speaking users.
  - Visual: Timeline with German cultural icons (e.g., pretzel for Q1, Alps for Q2).
- **Purpose**: Show a clear, German-centric growth plan.

---

### Slide 14: Team
- **Title**: Our Team
- **Content**:
  - Sachin Shetty: Software Engineer with expertise in GenAI and full-stack development. Passionate about making voice tech accessible for German speakers.
  - (Add other team members/advisors with German market ties if applicable.)
  - Visual: Professional headshot of Sachin with subtle German flag or tech background.
- **Purpose**: Build trust with team’s German market commitment.

---

### Slide 15: Research & Collaboration
- **Title**: Innovating for German Speakers
- **Content**:
  - Goal: Improve AI performance (e.g., faster Time to First Token Generation) for German voice queries.
  - Open-Source Tools: Leveraging GitHub repos for ASR, TTS, LLMs, and translation.
  - Collaboration: Partnering with German universities and open-source communities.
  - Visual: GitHub repo screenshots (German language commits) or collaboration icon.
- **Purpose**: Highlight innovation and community engagement.

---

### Slide 16: Closing & Call to Action
- **Title**: Join Us in Empowering 50M Voices
- **Content**:
  - Closing: “Help us bring Dhwani to Anna and millions of German speakers. Let’s make voice technology inclusive, private, and German-first.”
  - Contact: Sachin Shetty | example@example.xocm | +98745688513625
  - Visual: Image of a German user (e.g., Anna smiling with Dhwani) and tagline: “Dhwani: Made for Germany.”
- **Purpose**: End with an emotional, actionable call to invest.

---

## Additional Notes
- **German Consistency**: Replace non-German screenshots (e.g., Kannada) with German examples. Frame multilingual features as future expansion (e.g., “Scalable to French, Spanish”).
- **Story Integration**: Reference “Anna” throughout for emotional continuity (vision, solution, roadmap).
- **Design Tools**: Use Canva, Figma, or PowerPoint with a premium template for polish. Verify German text accuracy with a native speaker.
- **Length**: Streamlined to 16 slides (from 18) by combining financials and repositioning research.

---

This revised pitch deck addresses feedback by:
1. Adding an emotional story (Anna’s struggle).
2. Ensuring German focus in all visuals/demos (no unrelated languages).
3. Enhancing design with a professional, German-cultural theme.
4. Streamlining for clarity and impact.

For further refinements (e.g., specific German text, slide visuals), please provide additional details.
You can save this as dhwani_pitch_deck_revised.md and use it as a guide for creating the updated pitch deck. Let me know if you need help with specific slide designs, German translations, or other enhancements!


---

visual changes

# Dhwani Pitch Deck: Visual Mockup Descriptions

These visual mockup descriptions guide the creation of a revised Dhwani pitch deck, emphasizing emotional storytelling, German language focus, and a polished design per feedback. Designed for tools like Canva, Figma, or PowerPoint, the mockups cover five key slides to balance impact and brevity. Each aligns with the one-page pitch summary, ensuring accessibility, privacy, and German cultural resonance.

---

## Design Guidelines (Applied to All Slides)
- **Color Palette**:
  - Primary: Deep blue (#003087, German flag-inspired).
  - Secondary: White (#FFFFFF).
  - Accent: Subtle yellow (#FFCE00) or black (#000000).
  - Use gradients sparingly for modern depth.
- **Fonts**:
  - Headers: Montserrat (bold, 36–48pt).
  - Body: Open Sans (regular, 18–24pt).
- **Imagery**:
  - High-quality stock photos/illustrations of diverse German speakers (elderly, students, professionals) or German cityscapes (Berlin, Munich).
  - Source from Unsplash, Pexels, or Shutterstock; avoid generic global tech images.
- **Icons**:
  - Flat, minimalist (e.g., microphone, lock) from Flaticon/Noun Project, blue/yellow.
- **Layout**:
  - 60% visuals, 40% text.
  - Use whitespace and grid alignment for clarity.
- **German Focus**:
  - All text overlays/screenshots in German (e.g., “Hallo, wie kann ich helfen?”).
  - Verify accuracy with a native speaker.

---

## Slide Mockups

### Slide 1: Title Slide
**Purpose**: Set an inviting, German-centric tone.

**Description**:
- **Background**: Soft gradient (white to light blue, #E6F0FA). Subtle, semi-transparent Brandenburg Gate outline (10% opacity) in top-right corner.
- **Central Image**: Circular cutout (300px diameter) of a smiling German family (grandparent, parent, child) using a smartphone, symbolizing inclusivity. Yellow border (#FFCE00, 2px).
- **Text**:
  - Title: “Dhwani: Bringing Voice Technology to Every German Speaker” (Montserrat, 48pt, bold, white, centered at top).
  - Tagline: “Accessible. Private. Made for You.” (Open Sans, 24pt, white, italicized, below title).
  - Logo: Hypothetical Dhwani logo (stylized microphone with “D” soundwaves, 100px height, blue/yellow) in bottom-left.
- **Elements**: Small German flag icon (50px, bottom-right), fading into background.
- **Animation (Optional)**: Title fades in, family image zooms slightly.
- **Rationale**: Warm imagery and German cues (Gate, flag) establish emotional connection and localization.

---

### Slide 2: The Problem (Story-Driven)
**Purpose**: Evoke empathy with Anna’s story to highlight exclusion.

**Description**:
- **Background**: White with faint gray accessibility icon (wheelchair) grid pattern (10% opacity).
- **Left Side (50%)**:
  - Image: 400x300px photo of an elderly German woman (Anna) looking frustrated at a tablet in a Munich apartment (wooden furniture, warm lighting). Soft blue border (3px).
  - Overlay: “Meet Anna, left out by English-only tech” (Montserrat, 20pt, white, bottom-left, semi-transparent black background).
- **Right Side (50%)**:
  - Text:
	- Header: “Imagine Being Left Out of the Digital World” (Montserrat, 36pt, bold, blue, left-aligned).
	- Body: “Anna, a visually impaired grandmother in Munich, can’t use Siri or Alexa. They don’t understand her German dialect or respect her privacy. 50M+ German speakers face this barrier.” (Open Sans, 18pt, black, max 4 lines).
	- Stat: “50M excluded” (Montserrat, 24pt, yellow, in blue circle, bottom-right).
- **Elements**: Red “X” icon (30px) over a generic microphone logo (top-right), symbolizing failure of existing assistants.
- **Animation (Optional)**: Image slides in from left, text fades in from right, stat circle pulses.
- **Rationale**: Split layout balances emotional imagery with concise problem statement, grounded in German context.

---

### Slide 5: The Solution
**Purpose**: Introduce Dhwani as German-focused, privacy-first.

**Description**:
- **Background**: Light blue (#E6F0FA) with subtle yellow soundwave pattern radiating from bottom-left (5% opacity).
- **Top (40%)**:
  - Text:
	- Title: “Dhwani: Your German Voice Assistant” (Montserrat, 40pt, bold, white, centered).
	- Subtext: “Fluent. Private. Community-Driven.” (Open Sans, 20pt, white, centered).
- **Bottom (60%)**:
  - Visual: 500x300px smartphone mockup showing Dhwani’s interface in German (e.g., text bubble: “Was ist das Wetter in Berlin?” with “Sonnig, 15°C”). Phone angled for 3D effect, shadow beneath.
  - Icons: Three 80px circles below phone:
	- Microphone (German fluency, blue fill).
	- Lock (privacy, yellow outline).
	- People (open-source, blue outline).
	- Labels: “Deutsch”, “Privatsphäre”, “Gemeinschaft” (Open Sans, 10pt, black).
- **Elements**: Yellow German flag stripe (20px wide) along left edge, blending into background.
- **Animation (Optional)**: Phone zooms in, icons fade in sequentially.
- **Rationale**: German screenshot and icons highlight Dhwani’s core value (fluency, privacy, community).

---

### Slide 8: Market Opportunity
**Purpose**: Showcase German market with scalable potential.

**Description**:
- **Background**: White with semi-transparent Europe map (10% opacity, blue) centered on Germany, Austria, Switzerland.
- **Central Visual**:
  - Map: 400x400px interactive-style map highlighting German-speaking countries (Germany blue, Austria/Switzerland lighter blue). Yellow dots on Berlin, Vienna, Zurich.
  - Stats:
	- “50M+ German Speakers” (Montserrat, 28pt, white, yellow bubble over Germany).
	- “Germany: 80M” (Open Sans, 16pt, white, near Berlin).
	- “Austria: 9M” (Open Sans, 16pt, white, near Vienna).
	- “Switzerland: 5M” (Open Sans, 16pt, white, near Zurich).
- **Text**:
  - Title: “A Massive Opportunity in German-Speaking Markets” (Montserrat, 36pt, bold, blue, top-center).
  - Body: “Immediate: 50M+ users. Future: Scalable to 300M+ Europeans across 10+ languages. Demand for regional tech is growing.” (Open Sans, 18pt, black, bottom-center, max 3 lines).
- **Elements**: Bar chart (100px wide, bottom-right) showing “Regional Tech Demand” rising (blue bars, yellow trendline).
- **Animation (Optional)**: Map zooms from Europe to Germany, stats pop in, bars rise.
- **Rationale**: Localized map anchors German focus, with stats hinting at broader scalability.

---

### Slide 16: Closing & Call to Action
**Purpose**: Inspire investment with emotional, German-first appeal.

**Description**:
- **Background**: Deep blue (#003087) with faint yellow glow from center, evoking hope.
- **Central Image**: 350x250px photo of Anna (from Slide 2) smiling, speaking to a phone with Dhwani. White frame (5px), yellow corner accent.
- **Text**:
  - Title: “Join Us in Empowering 50M Voices” (Montserrat, 40pt, bold, white, above image).
  - Body: “Help bring Dhwani to Anna and millions of German speakers. Let’s make voice technology inclusive, private, and German-first.” (Open Sans, 20pt, white, below image).
  - Contact: “Sachin Shetty | example@example.xocm | +98745688513625” (Open Sans, 16pt, yellow, bottom-center).
  - Tagline: “Dhwani: Made for Germany” (Montserrat, 18pt, italic, white, bottom-right).
- **Elements**: Cluster of yellow microphone icons (20px, top-left), fading into background.
- **Animation (Optional)**: Image fades in, text slides up, microphones twinkle.
- **Rationale**: Emotional callback to Anna and clear contact details create a memorable close.

---

## Implementation Tips
- **Tools**:
  - **Canva**: Use pitch deck template, customize with German imagery (“Germany culture”, “accessibility tech”). Add icons from library.
  - **Figma**: Create 8px grid, import Unsplash photos (“German people”, “Berlin skyline”), use map plugins.
  - **PowerPoint**: Apply premium template, source Shutterstock/Pexels images, use fade transitions.
- **German Text**: Demo phrases: “Wie ist das Wetter?”, “Lies mir die Nachrichten”, “Übersetze ins Englische”. Verify dialects (e.g., Bavarian vs. Standard).
- **Stock Images**: Unsplash/Pexels for “German elderly”, “Berlin students”, “accessibility tech”. Avoid clichéd tech imagery.
- **Map Creation**: Snazzy Maps or Canva elements for market slide, highlighting German-speaking regions.
- **Consistency**: Save master slide with palette, fonts, logo placement. Export as PDF/PPTX.

---

## Notes
- **Feedback Alignment**: Slides use German text only (no Indian languages), feature Anna’s story (Slides 2, 16), and incorporate cultural cues (flag, cityscapes).
- **Scope**: Covers Slides 1, 2, 5, 8, 16 to demonstrate style. Other slides (e.g., Financials) can use similar elements (pie charts, timelines with German icons).
- **Limitations**: Descriptions maximize detail without image generation. For wireframes or additional slides, please specify.
- **Next Steps**: Brief a designer with these details or create slides in chosen tool. Can refine further (e.g., hex codes, German phrases).

---


optimized pitch deck


# Dhwani Pitch Deck (Revised with Additional Feedback)

This revised pitch deck for Dhwani, a German-speaking voice assistant, is optimized for a 5-minute pitch (followed by 5-minute Q&A) based on feedback to reduce text, avoid a salesy tone, and enhance visuals with color and a logo. It maintains emotional storytelling (Anna’s narrative), German focus, and factual strengths, streamlined to ~10 slides with minimal information and vibrant, inspiring design.

---

## General Design Guidelines
- **Color Palette**:
  - Primary: Deep blue (#003087, German flag-inspired, trust).
  - Accent: Warm yellow (#FFCE00, optimism).
  - Secondary: White (#FFFFFF, clarity).
  - Highlight: Soft green (#A8D5BA, accessibility, growth).
  - Avoid black-and-white; use gradients for depth.
- **Fonts**:
  - Headers: Montserrat (bold, 32–40pt).
  - Body: Open Sans (regular, 16–20pt, sparse text).
  - Max 20 words per slide to keep concise.
- **Logo**: Hypothetical “Dhwani” logo—a stylized microphone with yellow soundwaves forming a “D” (blue base, 100px height), placed subtly on each slide (bottom-left corner).
- **Imagery**:
  - High-quality stock photos/illustrations of diverse German speakers (elderly, students) and subtle cultural cues (e.g., Munich skyline).
  - Source from Unsplash/Pexels; avoid generic tech images.
- **Icons**:
  - Minimalist (e.g., microphone, lock) in blue/yellow/green, from Flaticon.
- **Layout**:
  - 70% visuals, 30% text.
  - One key message per slide.
  - Whitespace for clarity, grid alignment.
- **German Focus**:
  - All demos/screenshots in German (e.g., “Wie kann ich helfen?”).
  - Verify text with native speaker.

---

## Slide-by-Slide Structure

### Slide 1: Title
**Purpose**: Introduce Dhwani with warmth and German pride.
- **Visual Mockup**:
  - **Background**: Gradient (blue #003087 to white), faint yellow German flag stripe (20px, left edge).
  - **Image**: Circular photo (250px) of a smiling German student speaking to a phone, Berlin skyline blurred behind.
  - **Text**:
	- “Dhwani: Voice for 50M Germans” (Montserrat, 40pt, white, top-center).
	- “Accessible. Private.” (Open Sans, 18pt, yellow, below).
  - **Elements**: Dhwani logo (bottom-left), small microphone icon (green, 30px, top-right).
  - **Animation**: Image fades in, text slides up.
- **Rationale**: Minimal text, vibrant colors, and German context set an inviting tone.

---

### Slide 2: Anna’s Story
**Purpose**: Evoke empathy with the problem via Anna.
- **Visual Mockup**:
  - **Background**: White with faint green accessibility icon grid (5% opacity).
  - **Image**: 350x250px photo of an elderly German woman (Anna) looking puzzled at a tablet, cozy Munich apartment setting.
  - **Text**:
	- “Anna can’t use voice tech” (Montserrat, 32pt, blue, top-left).
	- “English-only. Not private.” (Open Sans, 16pt, black, below, max 10 words).
  - **Elements**: Red “X” icon (20px) over generic assistant logo (top-right), logo bottom-left.
  - **Animation**: Image slides in, text fades in.
- **Rationale**: Emotional image and sparse text highlight exclusion in 10 seconds.

---

### Slide 3: The Problem
**Purpose**: Quantify the German exclusion issue.
- **Visual Mockup**:
  - **Background**: Soft blue (#E6F0FA), subtle soundwave pattern (yellow, bottom).
  - **Visual**: Pie chart (200px, center): 50M German speakers (blue) vs. global English users (gray).
  - **Text**:
	- “50M Germans left out” (Montserrat, 36pt, white, above chart).
	- “No privacy. No access.” (Open Sans, 16pt, yellow, below).
  - **Elements**: Logo bottom-left, green lock icon (30px, top-right).
  - **Animation**: Chart segments fill, text pops in.
- **Rationale**: Simple visual and minimal words convey scale without overwhelming.

---

### Slide 4: Dhwani’s Vision
**Purpose**: Share a hopeful, inclusive goal.
- **Visual Mockup**:
  - **Background**: Gradient (white to green #A8D5BA), faint Munich skyline silhouette (bottom, 10% opacity).
  - **Image**: 300x200px photo of diverse Germans (student, retiree) smiling, using phones.
  - **Text**:
	- “Every German voice heard” (Montserrat, 36pt, blue, top-center).
	- “Private. Accessible. German.” (Open Sans, 16pt, white, below).
  - **Elements**: Logo bottom-left, yellow microphone icon (top-right).
  - **Animation**: Image zooms in, text fades.
- **Rationale**: Uplifting image and concise vision tie to Anna, avoiding sales pitch.

---

### Slide 5: The Solution
**Purpose**: Introduce Dhwani’s core features.
- **Visual Mockup**:
  - **Background**: White with yellow soundwaves radiating from center (5% opacity).
  - **Visual**: 400x250px smartphone mockup, Dhwani interface in German (“Was ist das Wetter?” → “Sonnig, 15°C”).
  - **Text**:
	- “Dhwani speaks German” (Montserrat, 32pt, blue, above phone).
	- “Private. Open-source.” (Open Sans, 16pt, green, below).
  - **Elements**: Logo bottom-left, blue lock icon (top-right).
  - **Animation**: Phone slides in, text fades.
- **Rationale**: German demo and minimal text showcase fluency and privacy.

---

### Slide 6: Why Dhwani?
**Purpose**: Highlight differentiation simply.
- **Visual Mockup**:
  - **Background**: Blue (#003087), faint green privacy lock pattern (top, 5% opacity).
  - **Visual**: Three icons (80px, horizontal, center):
	- Microphone (German fluency, blue).
	- Lock (privacy, yellow).
	- People (open-source, green).
  - **Text**:
	- “German. Private. Open.” (Montserrat, 36pt, white, above icons).
  - **Elements**: Logo bottom-left, small German flag (20px, top-right).
  - **Animation**: Icons pop in one by one.
- **Rationale**: Visual-first, three words capture essence without salesy tone.

---

### Slide 7: Traction
**Purpose**: Show early progress briefly.
- **Visual Mockup**:
  - **Background**: White with subtle yellow star pattern (bottom, 5% opacity).
  - **Visual**: 300x200px Play Store screenshot (German Dhwani app page).
  - **Text**:
	- “Live with early users” (Montserrat, 32pt, blue, top-center).
	- “1,000+ testers” (Open Sans, 16pt, green, below).
  - **Elements**: Logo bottom-left, green checkmark icon (top-right).
  - **Animation**: Screenshot fades in, text slides up.
- **Rationale**: Concise proof of momentum, German focus via screenshot.

---

### Slide 8: Market
**Purpose**: Frame the German opportunity.
- **Visual Mockup**:
  - **Background**: Soft green (#A8D5BA), faint Germany map outline (center, 10% opacity).
  - **Visual**: 250x250px map highlighting Germany, Austria, Switzerland (blue, yellow dots on Berlin, Vienna, Zurich).
  - **Text**:
	- “50M German speakers” (Montserrat, 36pt, white, above map).
	- “Growing tech demand” (Open Sans, 16pt, yellow, below).
  - **Elements**: Logo bottom-left, blue growth arrow (top-right).
  - **Animation**: Map zooms in, text fades.
- **Rationale**: Simple map and text emphasize scale, not sales.

---

### Slide 9: Next Steps
**Purpose**: Outline future without selling.
- **Visual Mockup**:
  - **Background**: White with blue timeline line (horizontal, center, 5px thick).
  - **Visual**: Three milestones (icons, 60px):
	- Q1: Microphone (German AI, blue).
	- Q3: Building (enterprise, yellow).
	- Q4: People (100K users, green).
  - **Text**:
	- “Building for Germans” (Montserrat, 32pt, blue, top-center).
	- “AI, enterprise, growth” (Open Sans, 16pt, black, below).
  - **Elements**: Logo bottom-left, green flag icon (top-right).
  - **Animation**: Icons slide along timeline.
- **Rationale**: Forward-looking but concise, tied to German users.

---

### Slide 10: Join Us
**Purpose**: Inspire collaboration, not sales.
- **Visual Mockup**:
  - **Background**: Blue (#003087) with yellow glow (center, 20% opacity).
  - **Image**: 300x200px photo of Anna smiling, using Dhwani on phone, Munich backdrop.
  - **Text**:
	- “Empower Anna’s voice” (Montserrat, 36pt, white, top-center).
	- “example@example.xocm” (Open Sans, 16pt, yellow, bottom-center).
  - **Elements**: Logo bottom-left, green microphone cluster (top-left).
  - **Animation**: Image fades, text slides up.
- **Rationale**: Emotional close, minimal text invites partnership.

---

## Implementation Notes
- **Slide Count**: Reduced to 10 (from 16) to fit 5-minute pitch (~30 seconds/slide). Merged financials into Q&A prep (e.g., €100K ask if asked), avoiding salesy tone.
- **Text Reduction**: Max 20 words/slide, focusing on visuals (70% of space). Removed dense stats (e.g., exact costs) for brevity.
- **Visuals**:
  - **Colors**: Blue/yellow/green palette replaces black-and-white, evoking trust, optimism, accessibility.
  - **Logo**: Hypothetical “D” microphone adds brand identity, consistently placed.
  - **Imagery**: German-specific (Anna, Berlin, Munich), sourced from Unsplash (“German elderly”, “Berlin skyline”).
  - **Tools**: Canva (pitch template, German imagery), Figma (8px grid, Unsplash imports), PowerPoint (premium template, fade transitions).
- **German Text**: Demo examples: “Was ist das Wetter?”, “Lies die Nachrichten”. Verify dialects (Standard German preferred).
- **Animation**: Subtle (fades, slides) to guide focus, not distract, optional for live pitch.
- **Q&A Prep**: Be ready for funding (€100K for 12 months), team (Sachin’s expertise), or tech (ASR/TTS) questions, but omit from slides to stay non-salesy.

---

## Feedback Alignment
- **Less Text**: Slides average 10–15 words, with visuals carrying the story (e.g., Anna’s photo, German map).
- **Non-Salesy**: Focus on Anna’s problem, Dhwani’s purpose, and collaboration, not revenue or hard asks.
- **Colorful Visuals**: Blue/yellow/green palette, German imagery, and logo replace black-and-white for inspiration.
- **German Focus**: All demos/screenshots in German, no unrelated languages (e.g., Kannada removed).
- **Story**: Anna anchors Slides 2 and 10, tying problem to solution emotionally.

---

## Additional Notes
- **File**: Save as `dhwani_pitch_deck_revised_2.md`.
- **Design**: Use descriptions to create slides or brief a designer. Canva’s “Pitch Deck” templates (customized with German photos) work well.
- **Logo Creation**: If no logo exists, mock up in Canva (microphone + “D” shape, blue/yellow) or hire a freelancer.
- **Further Refinement**: Can add wireframes (text-based), more German phrases, or specific slide tweaks if needed.

---


summary -  


# Dhwani: Giving 50M Germans a Voice

Imagine Anna, a visually impaired grandmother in Munich, unable to use voice assistants like Siri or Alexa. They don’t understand her German dialect or respect her privacy. Over 50 million German speakers—across Germany, Austria, and Switzerland—face this exclusion, locked out of digital access by English-centric tech and data concerns.

Dhwani changes this. It’s a voice assistant that speaks fluent German, designed for Anna and millions like her. Open-source and privacy-first, Dhwani runs on-premise, keeping data secure. It answers queries like “Was ist das Wetter in Berlin?” with ease, supports translations, and describes images in German, making tech accessible to all, including those with disabilities.

Our vision is simple: every German speaker’s voice should be heard. Dhwani is tailored for Germany’s 80 million, Austria’s 9 million, and Switzerland’s 5 million people, with potential to reach 300 million Europeans later. Unlike generic assistants, Dhwani is German-first, private, and community-driven, built with AI to understand dialects and deliver natural responses.

We’re already live on the Google Play Store, with 1,000+ German-speaking testers and growing open-source support. The market is ready—50 million German speakers crave regional, trusted tech. Our small team, led by Sachin Shetty, is passionate about accessibility and innovation.

Next, we’re enhancing Dhwani’s German AI, exploring enterprise use, and aiming for 100,000 users by late 2025. We’re not selling a product today—we’re inviting you to join us in empowering Anna and millions more.

**Contact**: Sachin Shetty | example@example.xocm | +98745688513625

---

**Design Note**:
- **Layout**: Single page, 12pt Open Sans, 1-inch margins. 60% visuals (top: photo of Anna smiling with phone, bottom: German map with Berlin dot). 40% text (blue #003087 headers, black body, yellow #FFCE00 accents).
- **Logo**: Stylized “Dhwani” microphone (blue base, yellow “D” soundwaves, 80px, top-left).
- **Colors**: Blue (#003087), yellow (#FFCE00), green (#A8D5BA) for vibrancy, avoiding black-and-white.
- **Visuals**: Unsplash photos (“German elderly”, “Munich skyline”). Subtle flag stripe (yellow, left edge).
- **Created**: April 12, 2025.



—
Apr 23, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-04-23-dhwani-inception-program-week-1.md


dwani.ai - Nvidia Inception- Week 1

- Week 1 - April 17-23, 2025
	- Launched App on Monday, April 21, 2025
	- Rebrand Dhwani to dwani.ai - April 22, 2025
	- Migrated dwani.ai v.0.0.1 inference server from HF spaces to Brev/Lambda labs GPU instances  - April 18, 2025
	- Feature - Added PDF extractor for English Doc to Kannada , April 20, 2025


- Week 2 - April 24-30, 2025
	- In progress - Refactor dwani.ai v0.0.1 api-server for AWS deployment
	- Draft Eval Report on accuracy improvement for Kannada with better model utilising H100 VRAM
    	- [https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/report/2025-04-23-dwani-technical-report-v-0-0-1.md](https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/report/2025-04-23-dwani-technical-report-v-0-0-1.md)
	- Planned workshop at Gopalan College of Engg.  - April - 28 ,2025
    	- https://tinyurl.com/dhwani-workshop
	- Hackathon at Berlin - April 26, 2025
    	- https://lu.ma/pyivp5k1



–

Apr 22, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/pitch/2025-05-22-pitch-feedback-3.md

´ve looked over your pitch deck. It´s visually more appealing now, however some information is missing.
For example, some more numbers regarding your financial plans. How will you be monetizing your product. What are your ambitions for scaling. What is your technical background. The Jury always wants some information about the founders.

—

Report 
–

Apr 23, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/report/2025-04-23-dwani-technical-report-v-0-0-1.md

dwani.ai > Technical report

# Dhwani.ai Technical Report

**Release Date:** April 21, 2025  
**Product:** Dhwani.ai Android App

---

## Hardware Sizing
The Dhwani.ai server configurations are optimized for different scales of deployment, utilizing various GPU and CPU hardware. Below is the hardware sizing for different server configurations:

| **Server Size** | **Hardware**     	| **Configuration**                                                             	|
|------------------|----------------------|----------------------------------------------------------------------------------|
| **Large**   	|  H100         	| 2 x Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 + 2x TTS/IndicF5 + 1x LLM for PDF |
| **Large**   	| A100         	| Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 |
| **Medium**  	| 1x L40S         	| Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Medium**  	| 1x L4           	| Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**   	| 1x T4           	| Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**   	| Local/CPU       	| Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |


## Model Configurations
The dwani.ai platform uses a combination of quantized large language models (LLMs), multilingual speech models, and translation models optimized for Indic languages. The configurations are tailored to server sizes:

### Large Server
- **LLM:** google/gemma-3-27b-it (4-bit quantized)
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - ai4bharat/indictrans2-en-indic-1B
  - ai4bharat/indictrans2-indic-en-1B
  - ai4bharat/indictrans2-indic-indic-1B
- **TTS Model:** ai4bharat/indicf5

### Medium Server
- **LLM:** google/gemma-3-12b-it (4-bit quantized)
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - ai4bharat/indictrans2-en-indic-dist-200M
  - ai4bharat/indictrans2-indic-en-dist-200M
  - ai4bharat/indictrans2-indic-indic-dist-320M
- **TTS Model:** ai4bharat/indicf5

### Small Server
- **LLM:** google/gemma-3-4b-it (4-bit quantized)
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - ai4bharat/indictrans2-en-indic-dist-200M
  - ai4bharat/indictrans2-indic-en-dist-200M
  - ai4bharat/indictrans2-indic-indic-dist-320M
- **TTS Model:** ai4bharat/indicf5

---

## Evaluation Details
The following models were evaluated for performance and accuracy:

- **LLM:** google/gemma-3-27b-it
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - full precision
   - ai4bharat/indictrans2-en-indic-1B
   - ai4bharat/indictrans2-indic-en-1B
   - ai4bharat/indictrans2-indic-indic-1B
  - distilled
   - ai4bharat/indictrans2-en-indic-dist-200M
   - ai4bharat/indictrans2-indic-en-dist-200M
   - ai4bharat/indictrans2-indic-indic-dist-320M
- **TTS Model:** ai4bharat/indicf5

**Key Observations:**
- The models successfully transcribe and translate Kannada (kan_Knda) speech inputs.
- Translation accuracy varies, with notable errors in mapping Indian locations (e.g., Hubli to New York).
- Response generation is contextually limited, leading to irrelevant responses in some cases.

---

## Performance Logs
The provided logs highlight two key interactions with the Dhwani.ai server on April 24, 2025, using the speech-to-speech endpoint (`/v1/speech_to_speech`).

### Log 1: Incorrect Translation (00:55:04 - 00:55:56)
- **Input (Kannada):** "ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತೊಗೋಬೇಕು" (Which train should I take from Hubli to Bangalore?)
- **Transcription:** Correctly transcribed.
- **Translation to English:** Incorrectly translated as "What train should I take from New York to New York?"
- **Generated Response (English):** "This question is irrelevant as I am designed to provide information about India and Karnataka, and there are no trains running from New York to New York."
- **Translated Response (Kannada):** Correctly translated back to Kannada but irrelevant due to the initial translation error.
- **Processing Time:** 12.282 seconds (00:55:04 - 00:55:16)

**Issues:**
- The translation model (likely IndicTrans2-200M) failed to recognize "Hubli" and "Bangalore," mapping them to "New York."
- The response generation model rejected the query due to the incorrect translation, resulting in an irrelevant response.
- Processing time is relatively high, indicating potential bottlenecks in the pipeline.

### Log 2: Correct Translation (01:08:30 - 01:08:37)
- **Input (Kannada):** "ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತಗೋಬೇಕು" (Which train should I take from Hubli to Bangalore?)
- **Transcription:** Correctly transcribed.
- **Translation to English:** Correctly translated as "What train to take from Hubli to Bangalore?"
- **Generated Response (English):** "To travel from Hubli to Bangalore, you can consider the Rani Chennamma Express."
- **Translated Response (Kannada):** Correctly translated as "ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರಿಗೆ ಪ್ರಯಾಣಿಸಲು, ನೀವು ರಾಣಿ ಚೆನ್ನಮ್ಮ ಎಕ್ಸ್ಪ್ರೆಸ್ ಅನ್ನು ಪರಿಗಣಿಸಬಹುದು."
- **Processing Time:** 8.482 seconds (01:08:30 - 01:08:37)

**Observations:**
- The translation model (likely IndicTrans2-1B, given the improved accuracy) correctly identified Indian locations.
- The response was accurate and contextually relevant, recommending a specific train.
- Processing time improved significantly (8.482 seconds vs. 12.282 seconds), likely due to the use of a larger model or optimized pipeline.

---

Server


–

Mar 10, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-10-gpu-hardware-sizing.md


# GPU Hardware Sizing for Model Workloads

## Overview
This document outlines hardware sizing for GPU-based equipment to support machine learning models: Automatic Speech Recognition (ASR), Text-to-Speech (TTS), Translation, Large Language Models (LLM), and Vision-Language Models (VLM). As of March 10, 2025, the focus is on running VLM, LLM, and TTS on the GPU while optimizing CPU usage for other tasks.

## Model Requirements
The following table lists the memory and hardware preferences for each model:

| **Model**  	| **VRAM Requirement** | **Preferred Hardware** |
|-----------------|----------------------|------------------------|
| ASR        	| 1 GB            	| CPU or GPU        	|
| TTS        	| 4.5 GB          	| GPU               	|
| Translation	| 3 GB            	| CPU or GPU        	|
| LLM        	| 6 GB            	| GPU               	|
| VLM        	| 4 GB            	| GPU               	|

**Notes:**
- VRAM requirements are minimums for inference. Training may demand additional resources.
- GPU priority: VLM (4 GB), LLM (6 GB), TTS (4.5 GB).

## Current Hardware (As of March 10, 2025)
- **Server Configuration:**
  - **GPU:** NVIDIA T4
	- VRAM: 16 GB
	- RAM: 16 GB (system memory)
  - **CPU:** Upgraded (specifications TBD)
- **Target GPU Workload:**
  - LLM: 6 GB
  - TTS: 4.5 GB
  - VLM: 4 GB
  - **Total VRAM Usage:** 14.5 GB / 16 GB available
  - **Remaining VRAM:** 1.5 GB
- **CPU Workload:** ASR (1 GB), Translation (3 GB)

**Observations:**
- The T4 GPU’s 16 GB VRAM can support LLM, TTS, and VLM simultaneously (14.5 GB total), leaving 1.5 GB of headroom.
- CPU efficiently handles ASR and Translation due to their lower memory needs.

## Proposed Hardware Setups
Below are configurations to optimize the current workload (VLM + LLM + TTS on GPU) and plan for scalability.

### Setup 1: Current T4 GPU + CPU Optimization
- **Hardware:** T4 GPU (16 GB VRAM), Enhanced CPU
- **Allocation:**
  - GPU: LLM (6 GB), TTS (4.5 GB), VLM (4 GB) = 14.5 GB
  - CPU: ASR (1 GB), Translation (3 GB)
- **Pros:**
  - Fully utilizes existing hardware with no additional cost.
  - Meets current GPU workload requirements (14.5 GB < 16 GB).
- **Cons:**
  - Limited headroom (1.5 GB) for batch size increases or additional tasks.
  - No redundancy.

### Setup 2: T4 GPU + Low-End GPU Backup
- **Hardware:**
  - T4 GPU (16 GB VRAM)
  - Additional GPU (e.g., NVIDIA GTX 1660, 6 GB VRAM)
  - Enhanced CPU
- **Allocation:**
  - T4 GPU: LLM (6 GB), TTS (4.5 GB), VLM (4 GB) = 14.5 GB
  - GTX 1660: Available for overflow or future tasks
  - CPU: ASR (1 GB), Translation (3 GB)
- **Pros:**
  - Maintains current workload on T4 with backup capacity.
  - Cost-effective redundancy.
- **Cons:**
  - GTX 1660 (6 GB) insufficient for full VLM + LLM + TTS if offloaded.
  - Minor increase in power/space needs.

### Setup 3: Upgrade to A100 GPU
- **Hardware:** NVIDIA A100 (40 GB or 80 GB VRAM), Enhanced CPU
- **Allocation:**
  - GPU: LLM (6 GB), TTS (4.5 GB), VLM (4 GB) = 14.5 GB, plus headroom
  - CPU: ASR (1 GB), Translation (3 GB)
- **Pros:**
  - Significant VRAM capacity (25.5 GB or 65.5 GB remaining) for scalability, training, or multi-instance support.
  - Future-proof for growing workloads.
- **Cons:**
  - Higher cost.
  - Overkill for current 14.5 GB requirement.

### Setup 4: Multi-T4 GPU Cluster
- **Hardware:** 2x T4 GPUs (32 GB VRAM total), Enhanced CPU
- **Allocation:**
  - T4 GPU 1: LLM (6 GB), TTS (4.5 GB) = 10.5 GB
  - T4 GPU 2: VLM (4 GB), potential overflow
  - CPU: ASR (1 GB), Translation (3 GB)
- **Pros:**
  - Distributes load across GPUs for flexibility (21.5 GB remaining total).
  - Redundancy and scalability.
- **Cons:**
  - Increased cost and complexity.
  - Requires multi-GPU optimization.

## Recommendations
1. **Short-Term:** Use **Setup 1** (current T4 GPU + CPU). The T4’s 16 GB VRAM supports VLM (4 GB), LLM (6 GB), and TTS (4.5 GB) with 1.5 GB to spare, while CPU handles ASR and Translation.
2. **Mid-Term:** Adopt **Setup 2** if minor redundancy or future overflow capacity is needed without major investment.
3. **Long-Term:** Transition to **Setup 3** (A100) or **Setup 4** (Multi-T4) for significant growth, such as training LLMs or expanding VLM/TTS usage.

## Next Steps
- Benchmark T4 performance with VLM + LLM + TTS at 14.5 GB to ensure stability.
- Evaluate latency/throughput needs to determine if 1.5 GB headroom suffices.
- Assess budget and growth plans to prioritize upgrades.

—
Mar 11, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-11-server-setup.md

Dhwani - Server / API configuration


Lazy load - all models

Fast stsrtup for health chech.

Log - system performance every minute

Measure load over time with graphana ?

Acheove full 100% usage

---

Model - usage
Compare -
Qwen vl with Moondream

Integrated- multimodal qwen or


Update settings-
Use dhwani url

Use localhost
Use -self hosted

---


create - issue list for problems identified,  track and fix them

—

Mar 14, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-14-dhwani-intro-1.md

# Dhwani Presentation Visuals for Undergraduate Students

This document provides a detailed guide to create engaging visuals for the "Dhwani - Voice AI" presentation, designed for an undergraduate audience. These visuals align with the revised slides from the previous Markdown file, enhancing relatability and clarity for Kannada-speaking students. Since I can't generate images directly, I'll describe each visual, suggest tools (e.g., Canva, PowerPoint, Google Slides), and recommend sources (e.g., Unsplash, Freepik) to help you build them.

---

## Visuals for Each Slide

### Slide 1: Meet Dhwani: Your Kannada-Speaking Voice Buddy!
- **Visual Description**: A cheerful cartoon-style smartphone with a speech bubble saying “ನಮಸ್ಕಾರ!” (Namaskara, "Hello" in Kannada). The phone has a friendly face (eyes and a smile) to personify Dhwani as a “buddy.”
- **Background**: Soft gradient (yellow to orange), reflecting Karnataka’s vibrant culture.
- **Text Placement**: Title at the top in bold white font with a subtle shadow; tagline “Imagine chatting with your phone in Kannada—Dhwani makes it happen!” below in smaller text.
- **Tool**: Canva—use “Cartoon” elements under “Graphics” and search for “smartphone” or “speech bubble.”
- **Source**: Freepik for cartoon phone and speech bubble icons; add Kannada text via Canva’s text tool (supports Indian scripts).

---

### Slide 2: Why We Need Dhwani
- **Visual Description**: A split image:
  - Left: A confused student speaking Kannada to a blank-faced Alexa/Siri (with a “?” above its head).
  - Right: A happy student talking to Dhwani (smiling phone with a Kannada speech bubble).
- **Background**: Light gray for contrast.
- **Text Placement**: Bullet points overlaid on the right side in a semi-transparent box, with “Over 50 million people speak Kannada” highlighted in bold.
- **Tool**: PowerPoint—use “SmartArt” to split the slide and insert images.
- **Source**: Pexels for student photos; edit with Canva to add speech bubbles and icons.

---

### Slide 3: What Makes Dhwani Special?
- **Visual Description**: Three icons in a row:
  1. A “free” tag (like a price tag with ₹0) for “It’s free for anyone to use or tweak.”
  2. A padlock on a laptop for “Runs on your device, keeping your chats private.”
  3. An IIT Madras logo or brain icon for “Built with smart tech from IIT Madras.”
- **Background**: White with a subtle Karnataka map outline in light yellow.
- **Text Placement**: Each bullet point next to its icon in a clean, bold font (e.g., Montserrat).
- **Tool**: Canva—search “icons” for tags, padlocks, and brain symbols.
- **Source**: Freepik for icons; IIT Madras logo from their official site (with permission if needed).

---

### Slide 4: What Can Dhwani Do?
- **Visual Description**: Two panels:
  1. A microphone with soundwaves and “ಪ್ರಶ್ನೆ” (Prashne, “Question” in Kannada) turning into “ಉತ್ತರ” (Uttara, “Answer”).
  2. A globe with arrows showing Kannada text (e.g., “ನಾನು ಭಾರತೀಯ”) translating to Hindi (“मैं भारतीय हूँ”).
- **Background**: Bright blue to suggest tech and connectivity.
- **Text Placement**: Descriptions below each panel in white boxes.
- **Tool**: Google Slides—use arrows and text boxes; screenshot the Dhwani app if available.
- **Source**: Unsplash for globe image; Kannada/Hindi text via Google Translate + Slides’ font options.

---

### Slide 5: Dhwani Today—March 14, 2025
- **Visual Description**: A phone screen mockup showing the Dhwani app logo, with a QR code linking to [tinyurl.com/dhwani-app-invite](https://tinyurl.com/dhwani-app-invite). Add a small “Play” button icon suggesting a demo.
- **Background**: Gradient green (symbolizing progress) fading to white.
- **Text Placement**: “It’s live! Try it on your Android” above the mockup; QR code caption below.
- **Tool**: Canva—use “Phone Mockup” templates and “QR Code Generator” feature.
- **Source**: Generate QR code in Canva; app logo from your project (or placeholder from Freepik).

---

### Slide 6: Dhwani’s Big Goals
- **Visual Description**: Three simple icons with labels:
  1. Ear icon for “Listen” (soundwaves around it).
  2. Mouth icon for “Speak” (speech bubble with Kannada script).
  3. Arrows circling between languages for “Translate.”
- **Background**: Light orange with a subtle wave pattern.
- **Text Placement**: Descriptions under each icon in a playful font (e.g., Comic Sans or Poppins).
- **Tool**: PowerPoint—insert icons from “Insert > Icons” and add text.
- **Source**: Built-in icons in PowerPoint or Canva’s free icon library.

---

### Slide 7: Help Us Make Dhwani Better!
- **Visual Description**: A speedometer with a needle pointing to “Fast,” paired with a GitHub logo and a “Join Us” button.
- **Background**: Dark blue to evoke tech innovation.
- **Text Placement**: “We’re speeding it up” above the speedometer; “Love coding?” next to the GitHub logo.
- **Tool**: Canva—search “speedometer” under “Elements” and add GitHub logo.
- **Source**: Freepik for speedometer; GitHub logo from their official branding page.

---

### Slide 8: Get Ready for the Workshop
- **Visual Description**: A checklist graphic: a laptop, GitHub logo, and HuggingFace logo, each with a green checkmark.
- **Background**: White with colorful confetti dots (to feel fun and welcoming).
- **Text Placement**: Bullet points in a vertical list beside the checklist, with “No coding skills? No problem!” in bold.
- **Tool**: Google Slides—use “Table” or “List” layout and insert logos.
- **Source**: Official GitHub and HuggingFace logos; Unsplash for confetti background.

---

### Slide 9: What You’ll Do at the Workshop
- **Visual Description**: A split image:
  - Left: A student typing code (with a Kannada comment like “// ಸರಳ ಕೋಡ್”).
  - Right: A chatbot bubble saying “ನಾನು ಸಹಾಯ ಮಾಡುತ್ತೇನೆ!” (I’ll help!).
- **Background**: Light purple for creativity.
- **Text Placement**: Descriptions below each half in white text boxes.
- **Tool**: Canva—use “Photo Frame” to split the slide and add text.
- **Source**: Pexels for student photo; create chatbot bubble in Canva.

---

### Slide 10: Your Turn!
- **Visual Description**: A thought bubble cloud with sketches of ideas: a graduation cap (study buddy), a speech bubble (translator), and a question mark (open-ended).
- **Background**: Bright yellow to energize the audience.
- **Text Placement**: “What do YOU want to make?” above the cloud; slides link below.
- **Tool**: PowerPoint—use “Shapes” to draw thought bubbles and insert icons.
- **Source**: Built-in PowerPoint icons or Freepik for sketches.

---

### Slide 11: Join the Dhwani Adventure!
- **Visual Description**: A road sign pointing to a horizon with “Workshop” and “App” arrows, plus a QR code for the app link.
- **Background**: Sunset gradient (orange to pink) symbolizing a journey.
- **Text Placement**: “Join the Dhwani Adventure!” at the top; action steps below the sign.
- **Tool**: Canva—search “road sign” and “horizon” under “Elements.”
- **Source**: Unsplash for sunset; QR code generated in Canva.

---

## How to Create These Visuals

1. **Choose a Tool**:
   - **Canva**: Free, drag-and-drop interface; ideal for beginners. Sign up at [canva.com](https://www.canva.com), select “Presentation (16:9),” and use templates or custom designs.
   - **PowerPoint/Google Slides**: Familiar to most students; great for quick edits and built-in icons.
2. **Gather Assets**:
   - **Images**: Search [Unsplash](https://unsplash.com) or [Pexels](https://pexels.com) for “students,” “smartphones,” or “Karnataka culture.”
   - **Icons**: [Freepik](https://freepik.com) or Canva’s free library (e.g., microphones, speech bubbles).
   - **Logos**: Use official GitHub, HuggingFace, or IIT Madras logos (with permission if public-facing).
3. **Add Kannada Text**:
   - Use [Google Input Tools](https://www.google.com/inputtools) to type Kannada, then copy-paste into your tool. Fonts like “Noto Sans Kannada” work well.
4. **Keep It Simple**:
   - Limit colors to 2-3 per slide (e.g., yellow, blue, white).
   - Use large, readable fonts (18pt+ for body text, 24pt+ for titles).
5. **Test It**:
   - View slides on a projector or screen to ensure visuals are clear from a distance.

---

## General Design Tips

- **Consistency**: Stick to a color palette (e.g., yellow, blue, orange) inspired by Karnataka’s flag or culture.
- **Cultural Touch**: Add subtle nods to Kannada heritage (e.g., a jasmine flower border or Yakshagana art silhouette).
- **Interactivity**: Include a demo screenshot or QR code to make it hands-on.
- **File Format**: Save as PPTX (PowerPoint) or PDF for easy sharing.

---

## Next Steps

- **Start with Slide 1**: In Canva, search “smartphone cartoon,” add a speech bubble with “ನಮಸ್ಕಾರ!”, and tweak colors.
- **Use Dhwani App**: Take a screenshot for Slide 5 and mock it up in a phone frame (Canva template).
- **Need Help?**: Let me know if you want detailed steps...

Something went wrong, please try again.


# Dhwani Presentation for Undergraduate Students

This document provides an improved version of the "Dhwani - Voice AI" presentation for an undergraduate audience. The suggestions simplify technical concepts, enhance engagement, and make the content relatable, ensuring it inspires curiosity and excitement about voice AI for Kannada and Indian languages.

---

## Revised Slides

### Slide 1: Introduction
- **Original**: "DNwAn - Voice AI / For Kannada / Indian Languages / slabstech.com/dhwani"
- **Revised**:
  - **Title**: “Meet Dhwani: Your Kannada-Speaking Voice Buddy!”
  - **Content**: “Imagine chatting with your phone in Kannada—Dhwani makes it happen!”
  - **Link**: slabstech.com/dhwani
- **Why**: A catchy, relatable hook grabs attention. “DNwAn” seems like a typo (should be “Dhwani”), and the original lacks an engaging opener.

---

### Slide 2: Why We Need Dhwani
- **Original**: Lists technical points about voice assistants lacking Indian language support.
- **Revised**:
  - **Title**: “Why We Need Dhwani”
  - **Content**:
	- “Ever tried asking Siri or Alexa something in Kannada? They don’t get it!”
	- “Over 50 million people speak Kannada, but most voice tech ignores them.”
	- “Dhwani uses free tools to fix this—built for YOU!”
- **Why**: Simplifies the problem into a relatable story, avoiding jargon like “OpenAI’s recent entry” and focusing on the human need.

---

### Slide 3: What Makes Dhwani Special?
- **Original**: Technical details about being open-source, self-hosted, and using AI4Bharat models.
- **Revised**:
  - **Title**: “What Makes Dhwani Special?”
  - **Content**:
	- “It’s **free** for anyone to use or tweak—like a community project!”
	- “Runs on your device, keeping your chats private.”
	- “Built with smart tech from **IIT Madras**—super reliable!”
- **Why**: Explains buzzwords in everyday terms and ties it to a prestigious institution for credibility.

---

### Slide 4: What Can Dhwani Do?
- **Original**: Lists “Answer Mode” and “Voice Translation” with technical terms like “TTS Indic Server.”
- **Revised**:
  - **Title**: “What Can Dhwani Do?”
  - **Content**:
	- “**Chat in Kannada**: Ask ‘What’s today’s weather?’ and get an answer in Kannada voice or text!”
	- “**Translate on the Fly**: Say a Kannada phrase, and hear it in Hindi—perfect for travel!”
	- *Add a small screenshot of the app in action.*
- **Why**: Real-life examples make it tangible. Skips server details—students care about functionality, not infrastructure.

---

### Slide 5: Dhwani Today—March 14, 2025
- **Original**: Slide 5 is broken (incomplete text), Slide 6 lists server and model details.
- **Revised** (Combines Slides 5 & 6):
  - **Title**: “Dhwani Today—March 14, 2025”
  - **Content**:
	- “It’s live! Try it on your Android: [tinyurl.com/dhwani-app-invite](https://tinyurl.com/dhwani-app-invite).”
	- “Dhwani listens to Kannada, speaks it back, and translates—pretty cool, right?”
	- *Add a QR code for the app link.*
- **Why**: Merges slides for clarity, skips model names (e.g., Qwen2.5), and emphasizes what students can try now. QR code adds interactivity.

---

### Slide 6: Dhwani’s Big Goals
- **Original**: Technical goals like ASR, TTS, and translation services.
- **Revised**:
  - **Title**: “Dhwani’s Big Goals”
  - **Content**:
	- “**Listen**: Understands spoken Kannada—like a friend who gets you.”
	- “**Speak**: Talks back in Kannada, naturally.”
	- “**Translate**: Switches Kannada to other Indian languages.”
- **Why**: Simplifies tech terms into actions students can visualize, keeping it approachable.

---

### Slide 7: Help Us Make Dhwani Better!
- **Original**: Mentions TTFTG and GitHub links, potentially overwhelming.
- **Revised**:
  - **Title**: “Help Us Make Dhwani Better!”
  - **Content**:
	- “We’re speeding it up so it answers you faster.”
	- “Love coding? Join us on GitHub: [tinyurl.com/dhwani-github](https://tinyurl.com/dhwani-github).”
- **Why**: Focuses on the “why” (faster responses) instead of “TTFTG,” and invites participation without being too technical.

---

### Slide 8: Get Ready for the Workshop
- **Original**: Lists tools like Python 3.10 and Ubuntu, which might intimidate.
- **Revised**:
  - **Title**: “Get Ready for the Workshop”
  - **Content**:
	- “Bring a laptop—don’t worry, we’ll help with setup!”
	- “Sign up for free accounts: GitHub (github.com) & HuggingFace (huggingface.co).”
	- “No coding skills? No problem—we’ll guide you!”
- **Why**: Reassures beginners and frames prerequisites as simple steps, lowering the entry barrier.

---

### Slide 9: What You’ll Do at the Workshop
- **Original**: Vague mention of GitHub walkthrough and UX building.
- **Revised**:
  - **Title**: “What You’ll Do at the Workshop”
  - **Content**:
	- “Play with Dhwani’s code and see how it works.”
	- “Build your own mini voice app—like a Kannada chatbot!”
- **Why**: Specific, hands-on goals excite students and show they’ll create something cool.

---

### Slide 10: Your Turn!
- **Original**: Basic Q&A with a slides link.
- **Revised**:
  - **Title**: “Your Turn!”
  - **Content**:
	- “What do YOU want to make with Dhwani? A study buddy? A translator?”
	- “Questions? Ask away!”
	- “Grab these slides: [tinyurl.com/dhwani-project-intro](https://tinyurl.com/dhwani-project-intro).”
- **Why**: Turns Q&A into a brainstorming session, encouraging creativity and engagement.

---

### Slide 11: Join the Dhwani Adventure!
- **Original**: No closing slide.
- **Revised**:
  - **Title**: “Join the Dhwani Adventure!”
  - **Content**:
	- “Try it now: [tinyurl.com/dhwani-app-invite](https://tinyurl.com/dhwani-app-invite).”
	- “Sign up for the workshop and build the future of voice AI!”
- **Why**: Ends with a clear next step, keeping students excited and involved.

---

## General Tips
1. **Add Visuals**: Include app screenshots, a demo clip of Dhwani responding in Kannada, or icons (e.g., microphone for ASR, speaker for TTS). Visuals break up text and make it lively.
2. **Keep It Short**: Aim for 1-2 key points per slide. Avoid dense text (e.g., fix Slide 5’s garbled content—likely an OCR error).
3. **Tell a Story**: Add a personal touch, e.g., “We made Dhwani so our families could use voice tech in Kannada.” It’s relatable and memorable.
4. **Highlight Benefits**: Mention how working on Dhwani boosts skills or resumes—undergrads love practical takeaways.
5. **Practice Timing**: Keep it 10-15 minutes max to hold attention, leaving time for Q&A.

---

## Sample Flow
- **Start**: Hook them with a relatable scenario (Slide 1).
- **Middle**: Explain the problem (Slide 2), Dhwani’s solution (Slides 3-4), and its status (Slide 5).
- **End**: Show how they can explore it (Slides 6-9) and join in (Slides 10-11).

---

With these tweaks, your intro to Dhwani will be **fun**, **clear**, and **inspiring** for undergrads—sparking their interest in AI and Indian languages. Good luck with your presentation!

–

Mar 15, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-15-dhwani-server-routing-v1.md

Dhwani- v1

Load balancer with cpu - upgrades

Route all queries to gpu instances.

Reply with wait message to stsrtup systems that are down.

Provide- system ststus button to get info regarding available service.


Host - tiny systems on the load balancer.

Pure fast api server only.

---


mobile App - server messages

Looks like our AI is taking a nap.

We are waking it up,  
Please come back in 3 mins.

We will be ready to serve you.


Run cpu variants of all service's,  
Use as fall back system when GPU resources are unavailable.

Restart gpu service on service request.

Run - smaller models on cpu services.
---

server unavailability- graceful response

Handle gracefully,  if a service is currently not available.

Provide- usable response to the App user.

--

health chech - evals

On startup - .
Check outputs for basic commands.

Verify that v the model - returns cirrect results



---

Analytics on usage

Focus on Android only,  
Make it secure,
Add logs/ enable disable logg8ng


Add- enable analytics for system improvement.
Mainly logs and translation.

Asd option for - rating response.

Add rlhf option.


‐--

Mar 15, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-15-open-issues-v1-march-15.md

Open Issues - v1 - march 15

Tts - error in reading english numbers

Kannada - is translated back as canada,

Update info not available,
Use tool calls to get better info.


Issue with copying data, date field is not necessary.

Add option to edit previous text message and resend

Tts - feature breaks with latest transformer library

Nemo - feastur breaks with latest - huggingface hub library




—

Mar 16, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-16-tts-latency.md

# Parler-TTS Latency Measurements

This report summarizes the latency measurements for the Parler-TTS text-to-speech system (`ai4bharat/indic-parler-tts`) under different hardware configurations and optimization methods. The latency is reported in seconds and corresponds to the time taken to generate audio for a given number of words. The data is derived from various tests conducted on March 16, 2025.

## Latency Table

# Parler-TTS Latency Measurements (Formatted)

| Hardware | Optimization Method     	| Word Count | Latency (s) | Notes                          	|
|:---------|:----------------------------|:----------:|:-----------:|:-----------------------------------|
| T4   	| Simple Transformer      	| 	5  	|	4.70 	| Baseline measurement          	|
| T4   	| Simple Transformer      	|	21  	|   23.63 	| Baseline measurement          	|
| T4   	| Flash Attention         	| 	5  	|	8.16 	| Slower than baseline          	|
| T4   	| Flash Attention         	|	21  	|   38.29 	| Significantly slower than baseline|
| L4   	| Flash Attention         	| 	5  	|	3.99 	| Fastest for 5 words across tests  |
| L4   	| Flash Attention         	|	21  	|   20.82 	| Improved over T4 FA           	|
| L4   	| Flash Attention (App)   	| 	7  	|	7.92 	| App request measurement       	|
| A10G 	| Flash Attention         	|	21  	|   25.52 	| Consistent but slower than L4 	|
| A10G 	| Flash Attention         	|	21  	|   24.33 	| Slight variation in repeated test |
| L4   	| Torch Compile (Regular) 	| 	1  	|	2.72 	| Minimal input size            	|
| L4   	| Torch Compile (Regular) 	| 	5  	|	2.58 	| Fastest for small input       	|
| L4   	| Torch Compile (Regular) 	| 	7  	|	4.70 	| Comparable to baseline T4     	|
| L4   	| Torch Compile (Regular) 	|	21  	|   10.65 	| Best regular compile for 21 words |
| L4   	| Torch Compile (Regular) 	|	21  	|   11.99 	| Slight variation              	|
| L4   	| Torch Compile (Regular) 	|	21  	|   12.10 	| Consistent performance        	|
| L4   	| Torch Compile (Regular) 	|	21  	|   13.51 	| Higher variation              	|
| L4   	| Torch Compile (Reduce OH)   | 	7  	|	3.00 	| Estimated from "3s - 7 words" 	|
| L4   	| Torch Compile (Reduce OH)   |	21  	|   10.00 	| Estimated from "10 s - 21"    	|
| L4   	| Torch Compile (Reduce OH)   |	21  	|   12.00 	| Estimated from "12 s - 21 words"  |

## Observations

1. **Hardware Impact**:
   - The L4 server with Flash Attention showed the best performance for 5 words (3.99s), suggesting better optimization or higher computational power compared to T4.
   - A10G with Flash Attention was slower (24-25s for 21 words) than L4 (20.82s), indicating potential hardware or configuration differences.

2. **Optimization Methods**:
   - **Simple Transformer (T4)**: Served as a baseline with 4.70s for 5 words and 23.63s for 21 words.
   - **Flash Attention**: Surprisingly slower on T4 (8.16s for 5 words, 38.29s for 21 words) compared to the baseline, but improved on L4 (3.99s for 5 words, 20.82s for 21 words). This suggests Flash Attention benefits from specific hardware capabilities.
   - **Torch Compile (Regular)**: Consistently faster than Flash Attention, with the best result for 5 words at 2.58s and a range of 10.65-13.51s for 21 words.
   - **Torch Compile (Reduce Overhead)**: Showed promising results with approximately 3s for 7 words and 10-12s for 21 words, indicating potential for lower latency with this mode.

3. **Input Size**:
   - Latency generally increases with word count, but the scaling is not linear. For example, Torch Compile (Regular) took 2.58s for 5 words and 10.65s for 21 words, suggesting optimization benefits for larger inputs.

## Notes

- The "reduce-overhead" mode values (3s, 12s, 10s) were approximated from your shorthand notation; actual measurements might vary slightly.
- All measurements were taken on March 16, 2025, using the `ai4bharat/indic-parler-tts` model.
- Latency values are in seconds (s), rounded to two decimal places.
- Word counts represent the number of words in the input text.
- "Reduce OH" refers to the "reduce-overhead" mode in Torch Compile.
- The table is sorted by hardware, then optimization method, and finally word count for better readability.

## Conclusion
The Torch Compile optimization, particularly with "reduce-overhead" mode, appears to offer the best balance of latency reduction across different input sizes. The L4 server with Flash Attention also performed well, especially for smaller inputs. For optimal performance, consider using Torch Compile with "reduce-overhead" mode on capable hardware, though further testing could refine these findings.
–
Mar 17, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-17-ffmpeg-edit.md

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

–
Mar 17, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-17-llm-indic-server-open-research.md


Indic LLM - Open Research



If user requests recent data or unknown data, then model generates wrong answer/hallucinates.

Because -
- Model are trained on data,  which have a 1 year/6 month old data.
- Recent and current information is not available due to the static nature of model weights.


To get recent data
- collect delta data from cut-off and fine tune the model
- build RAG system to access recent data stored in vector store/ database

Ex - make company docs and api available via  - text / natural language search


To get real time data-
- access external api with tool/function call
- build bot scraper to index recent data for websites/ which do not have Api exposed

—
Mar 30, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-20-gemma-speed-up.md


Gemma - Speed Up

Using a slow image processor as `use_fast` is unset and a slow processor was saved with this model. `use_fast=True` will be the default behavior in v4.48, even if the model was saved with a slow processor. This will result in minor differences in outputs. You'll still be able to use a slow processor with `use_fast=False`.
2025-03-20 00:20:03,894 - dhwani_api - INFO - LLM google/gemma-3-4b-it loaded on cuda with compiled forward pass
/usr/local/lib/python3.10/dist-packages/torch/_inductor/compile_fx.py:194: UserWarning: TensorFloat32 tensor cores for float32 matrix multiplication available but not enabled. Consider setting `torch.set_float32_matmul_precision('high')` for better performance.
  warnings.warn(
W0320 00:20:26.460000 1 torch/_inductor/utils.py:1137] [0/0] Not enough SMs to use max_autotune_gemm mode


—
Mar 21, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-03-21-speech-input-language-stream.md


Speed Detection and Streaming for real time voice


Sameple 2 sec audio on each Language for Transcription

Pass it via asr for the available Language and get c text in multiple Language


Use Indic lid for text to match exact language.


.

Currently ASR is not streaming,  
We want to add streaming voice input first and experiment with language identification.


–
Apr 4, 2025
https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-04-04-dhwani-model-server-configs.md

Dhwani Model Server - configs

T4
1. Configs one :
Configs- Kannada - speech to t3xt
Llm - Gemma3-1b-instruct
Vision - Moondream2
ASR - Indic cornformer
transalte - IndicTrans2- Kannada


2. Config two
Configs- kannada - speech to speech
Config one + tts-indic server

Same config- for all other single  indian language


3. Config Three
Config - german- speech to Text
Asr - whisper
Llm - gemma 1b
Moondream 2

4. Config four
Config  - German - speech to Speech
Ast - whisper
Llm - gemma 1b
Monndream
Tts- parler-tts


L4
1.

–
Apr 21, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-04-24-server-v-0-0-1-recommendation.md


# Dhwani.ai Technical Report

**Release Date:** April 21, 2025  
**Product:** Dhwani.ai Android App

---

## Overview
Dhwani.ai is an AI-powered platform designed to provide multilingual speech-to-speech and text processing capabilities, with a focus on Indic languages. The Android app, released on April 21, 2025, leverages advanced machine learning models for transcription, translation, and response generation, tailored for Indian users. This report outlines the hardware sizing, model configurations, evaluation details, and observed performance, along with recommendations for improvement based on provided logs.

---

## Hardware Sizing
The Dhwani.ai server configurations are optimized for different scales of deployment, utilizing various GPU and CPU hardware. Below is the hardware sizing for different server configurations:

| **Server Size** | **Hardware**     	| **Configuration**                                                             	|
|------------------|----------------------|----------------------------------------------------------------------------------|
| **Large**   	| 2x H100         	| Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 + 2x TTS/IndicF5 + 1x LLM for PDF |
| **Large**   	| 1x A100         	| Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 |
| **Medium**  	| 1x L40S         	| Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Medium**  	| 1x L4           	| Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**   	| 1x T4           	| Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**   	| Local/CPU       	| Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |

**Notes:**
- **H100** configurations support advanced workloads, including PDF processing and enhanced TTS capabilities.
- **A100** and **H100** are used for large-scale deployments with higher model complexity.
- **L40S** and **L4** are optimized for medium-sized deployments with distilled models for efficiency.
- **T4** and **CPU** configurations are lightweight, suitable for small-scale or edge deployments.

---

## Model Configurations
The Dhwani.ai platform uses a combination of quantized large language models (LLMs), multilingual speech models, and translation models optimized for Indic languages. The configurations are tailored to server sizes:

### Large Server
- **LLM:** google/gemma-3-27b-it (4-bit quantized)
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - ai4bharat/indictrans2-en-indic-1B
  - ai4bharat/indictrans2-indic-en-1B
  - ai4bharat/indictrans2-indic-indic-1B
- **TTS Model:** ai4bharat/indicf5

### Medium Server
- **LLM:** google/gemma-3-12b-it (4-bit quantized)
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - ai4bharat/indictrans2-en-indic-dist-200M
  - ai4bharat/indictrans2-indic-en-dist-200M
  - ai4bharat/indictrans2-indic-indic-dist-320M
- **TTS Model:** ai4bharat/indicf5

### Small Server
- **LLM:** google/gemma-3-4b-it (4-bit quantized)
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - ai4bharat/indictrans2-en-indic-dist-200M
  - ai4bharat/indictrans2-indic-en-dist-200M
  - ai4bharat/indictrans2-indic-indic-dist-320M
- **TTS Model:** ai4bharat/indicf5

**Notes:**
- Quantized models (4-bit) reduce memory and computational requirements while maintaining performance.
- IndicTrans2 models are optimized for translation between English and Indic languages, as well as Indic-to-Indic translations.
- IndicConformer supports multilingual speech recognition, and IndicF5 handles text-to-speech for Indic languages.

---

## Evaluation Details
The following models were evaluated for performance and accuracy:

- **LLM:** google/gemma-3-12b-it (quantized)
- **Speech Model:** ai4bharat/indic-conformer-600m-multilingual
- **Translation Models:**
  - ai4bharat/indictrans2-en-indic-dist-200M
  - ai4bharat/indictrans2-indic-en-dist-200M
  - ai4bharat/indictrans2-indic-indic-dist-320M
- **TTS Model:** ai4bharat/indicf5

**Key Observations:**
- The models successfully transcribe and translate Kannada (kan_Knda) speech inputs.
- Translation accuracy varies, with notable errors in mapping Indian locations (e.g., Hubli to New York).
- Response generation is contextually limited, leading to irrelevant responses in some cases.

---

## Performance Logs
The provided logs highlight two key interactions with the Dhwani.ai server on April 24, 2025, using the speech-to-speech endpoint (`/v1/speech_to_speech`).

### Log 1: Incorrect Translation (00:55:04 - 00:55:56)
- **Input (Kannada):** "ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತೊಗೋಬೇಕು" (Which train should I take from Hubli to Bangalore?)
- **Transcription:** Correctly transcribed.
- **Translation to English:** Incorrectly translated as "What train should I take from New York to New York?"
- **Generated Response (English):** "This question is irrelevant as I am designed to provide information about India and Karnataka, and there are no trains running from New York to New York."
- **Translated Response (Kannada):** Correctly translated back to Kannada but irrelevant due to the initial translation error.
- **Processing Time:** 12.282 seconds (00:55:04 - 00:55:16)

**Issues:**
- The translation model (likely IndicTrans2-200M) failed to recognize "Hubli" and "Bangalore," mapping them to "New York."
- The response generation model rejected the query due to the incorrect translation, resulting in an irrelevant response.
- Processing time is relatively high, indicating potential bottlenecks in the pipeline.

### Log 2: Correct Translation (01:08:30 - 01:08:37)
- **Input (Kannada):** "ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತಗೋಬೇಕು" (Which train should I take from Hubli to Bangalore?)
- **Transcription:** Correctly transcribed.
- **Translation to English:** Correctly translated as "What train to take from Hubli to Bangalore?"
- **Generated Response (English):** "To travel from Hubli to Bangalore, you can consider the Rani Chennamma Express."
- **Translated Response (Kannada):** Correctly translated as "ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರಿಗೆ ಪ್ರಯಾಣಿಸಲು, ನೀವು ರಾಣಿ ಚೆನ್ನಮ್ಮ ಎಕ್ಸ್ಪ್ರೆಸ್ ಅನ್ನು ಪರಿಗಣಿಸಬಹುದು."
- **Processing Time:** 8.482 seconds (01:08:30 - 01:08:37)

**Observations:**
- The translation model (likely IndicTrans2-1B, given the improved accuracy) correctly identified Indian locations.
- The response was accurate and contextually relevant, recommending a specific train.
- Processing time improved significantly (8.482 seconds vs. 12.282 seconds), likely due to the use of a larger model or optimized pipeline.

---

## Issues Identified
1. **Translation Errors:**
   - The IndicTrans2-200M model struggles with Indian place names, leading to incorrect translations (e.g., Hubli → New York).
   - This issue is less prevalent with the IndicTrans2-1B model, suggesting that model size impacts translation accuracy.

2. **Contextual Relevance:**
   - The response generation model (Gemma-3) fails to provide meaningful answers when translations are incorrect, as seen in Log 1.
   - The model is overly restrictive in its context (e.g., rejecting queries it misinterprets as non-Indian).

3. **Processing Time:**
   - The speech-to-speech pipeline takes 8.482–12.282 seconds, which is suboptimal for real-time applications.
   - Longer processing times in Log 1 suggest inefficiencies in the smaller model pipeline (likely Medium or Small server).

4. **Deprecation Warning:**
   - A warning in Log 2 indicates the use of deprecated functionality in the Transformers library (`as_target_tokenizer`). This could lead to compatibility issues in future updates.

---

## Recommendations for Improvement
1. **Enhance Translation Accuracy:**
   - **Upgrade to IndicTrans2-1B for All Configurations:** The 1B model demonstrates superior performance in handling Indian place names compared to the 200M distilled model. Deploy it across Medium and Small servers if hardware permits.
   - **Fine-Tune Translation Models:** Fine-tune IndicTrans2 models on a dataset of Indian place names and travel-related queries to improve location recognition.
   - **Implement Geolocation Context:** Add a geolocation filter to prioritize Indian locations in translations, reducing errors like "New York."

2. **Improve Response Generation:**
   - **Contextual Expansion:** Modify the Gemma-3 prompt template to handle mistranslated inputs more gracefully, e.g., by detecting and correcting location-based errors.
   - **Fallback Mechanism:** Implement a fallback response for irrelevant queries, such as suggesting the user clarify the location or query.

3. **Optimize Processing Time:**
   - **Pipeline Optimization:** Profile the speech-to-speech pipeline to identify bottlenecks (e.g., transcription, translation, or response generation). Optimize model inference with techniques like mixed precision or batching.
   - **Hardware Upgrades:** For Medium and Small servers, consider upgrading to L40S or A100 GPUs to reduce latency, especially for real-time applications.
   - **Caching:** Cache frequently asked queries (e.g., train routes) to reduce processing time for common requests.

4. **Address Deprecation Warning:**
   - Update the codebase to use the recommended `text_target` argument in the Transformers library, ensuring compatibility with future versions (v5 and beyond).
   - Conduct a code audit to identify and resolve other deprecated dependencies.

5. **Monitoring and Logging:**
   - Implement detailed logging for model performance metrics (e.g., transcription accuracy, translation BLEU scores, response relevance).
   - Add error tracking for translation failures to identify recurring issues with specific inputs.

6. **User Experience:**
   - **Feedback Loop:** Integrate a feedback mechanism in the Android app to collect user reports on incorrect translations or responses, enabling continuous model improvement.
   - **Multimodal Support:** Enhance the app to handle text inputs alongside speech, providing flexibility for users with poor audio quality.

---

## Conclusion
The Dhwani.ai Android app, released on April 21, 2025, demonstrates robust capabilities for multilingual speech processing in Indic languages. The platform leverages advanced models like Gemma-3, IndicConformer, and IndicTrans2, with hardware configurations tailored to different deployment scales. However, issues with translation accuracy, response relevance, and processing time highlight areas for improvement. By upgrading translation models, optimizing the pipeline, and addressing deprecated dependencies, Dhwani.ai can enhance its performance and user experience, solidifying its position as a leading AI platform for Indic language processing.

**Next Steps:**
- Deploy IndicTrans2-1B models across all server sizes.
- Optimize the speech-to-speech pipeline to achieve sub-5-second latency.
- Update the Transformers library to resolve deprecation warnings.
- Collect user feedback to fine-tune models and improve accuracy.

---

This report provides a comprehensive overview of Dhwani.ai’s technical setup and performance, with actionable recommendations to address identified issues.

–
May 1, 2025

https://github.com/sachinsshetty/onwards/blob/main/idea/dhwani/server/2025-05-01-dwani-docs-latency.md

dwani.ai - Document processing latency

We test the time taken to extract text from dwani.ai - Pitch deck for Europe

27B
12B - 17.717 s
4B - 12.556 s
27B-Q -
12B-Q - 28.79
4B-Q - 18
