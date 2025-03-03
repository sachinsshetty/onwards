# Project Dhwani: Enhancing Kannada Voice Model Development with GPU Access

## Table of Contents

1. [Executive Summary](#executive-summary)
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
11. [ChangeLog](#changelog)
    - [v.0.0.1 - 25 Feb - 3 Mar 2025](#v001)

## Executive Summary

The primary research goal of Project Dhwani is to measure and improve the Time to First Token Generation (TTFTG) for model architectures in Automatic Speech Recognition (ASR), Translation, and Text-to-Speech (TTS) systems. By leveraging open-source Large Language Models (LLMs) and tools provided by AI4BHARAT, we aim to develop and enhance a Kannada voice model that meets industry standards set by Alexa, Siri, and Google. The project will focus on creating robust voice solutions for Indian languages, with a specific emphasis on Kannada. To achieve this, we require GPU access for a period of three months. Therefore, we request a research grant/sponsorship of $960 per month for 3 months. Total grant request would be $2880 to support this endeavor.


## Introduction

### Background

Current voice assistants like Alexa, Siri, and Google dominate the consumer market but lack comprehensive support for Indian languages, particularly Kannada. OpenAI's recent entry into the voice assistant market highlights the growing demand for such technologies. By utilizing open-source models and tools, we can develop a voice solution that is accessible and robust, specifically tailored for Kannada speakers.

### Objectives

The primary objective is to integrate and enhance the following models and services for Kannada:
- **Automatic Speech Recognition (ASR)**: To convert spoken Kannada into text.
- **Text-to-Speech (TTS)**: To convert Kannada text into natural-sounding speech.
- **Translation Services**: To enable translation between Kannada and other Indian languages.

## Target Solution

| Answer Engine                                  | Voice Translation                          |
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
| Month | Activity                          | Users | Cost per Hour/GPU ($) | Hours per Day | Daily Cost ($) | Monthly Cost ($) |
|-------|-----------------------------------|-------|-----------------------|---------------|----------------|------------------|
| 1     | Development and optimization      | 1-5   | 0.5                   | 4             | 2.00           | 960              |
| 2     | Scalability tests and beta users | 10-20 | 0.5                   | 24            | 12.00          | 960              |
| 3     | Large scale testing across timezones | 10-20 | 0.5                   | 36            | 18.00          | 960              |

**Total Cost**
- **Total Cost**: $960 + $960 + $960 = $2,880

## Project Scope

### Models and Tools
The project will utilize the following open-source tools:

| Open-Source Tool                       | Source Repository                                          | CPU / Available 24/7 - Free, Slow | GPU / Paused, On-demand, $.05 /hour |
|---------------------------------------|-------------------------------------------------------------|----------------|----------------|
| Automatic Speech Recognition : ASR   | [ASR Indic Server](https://github.com/slabstech/asr-indic-server) | [HF Demo](https://huggingface.co/spaces/gaganyatri/asr_indic_server_cpu) |  [Ondemand - HF Demo](https://huggingface.co/spaces/gaganyatri/asr_indic_server)  |
| Text to Speech : TTS                  | [TTS Indic Server](https://github.com/slabstech/tts-indic-server)  | [HF Demo](https://huggingface.co/spaces/gaganyatri/tts_indic_server_cpu)            | [Ondemand - HF Demo](https://huggingface.co/spaces/gaganyatri/asr_indic_server) |
| Translation                           | [Indic Translate Server](https://github.com/slabstech/indic-translate-server) | [HF Demo](https://huggingface.co/spaces/gaganyatri/translate_indic_server_cpu)          | [Ondemand - HF Demo](https://huggingface.co/spaces/gaganyatri/translate_indic_server)            |

### Current Setup

The development is currently being executed on a laptop with a GTX 1060 6GB VRAM. However, to ensure robustness and scalability, additional GPU resources are required.


#### Integrated Demos
- Demo for Testing components for Dhwani for Accuracy and evaluation

| Feature                      | Description                                                                 | Demo Link | Components          | Source Code       |
|------------------------------|-----------------------------------------------------------------------------|-----------|---------------------|-------------------|
| Answer Engine                | Provides answers to queries using a large language model.                     |   | LLM                 | [Link](https://github.com/slabstech/dhwani/ux/answer_engine/app.py)          |
| Answer Engine with Translate| Provides answers to queries with translation capabilities.                   | [Link](https://huggingface.co/spaces/gaganyatri/dhwani-voice-model)  | LLM, Translation    | [Link](https://github.com/slabstech/dhwani/ux/answer_engine_translate/app.py)          |
| PDF Translate                | Translates content from PDF documents.                                       |  | Translation         |           |
| Text Translate               | Translates text from one language to another.                                |   | Translation         |           |
| Voice Generation            | Generates speech from text.                                                  |   | TTS                 | [Link](https://github.com/slabstech/dhwani/ux/text_to_speech/app.py)          |
| Voice to Text Translation    | Converts spoken language to text and translates it.                          | [Link](https://huggingface.co/spaces/gaganyatri/dhwani-tts)  | ASR, Translation    | [Link](https://github.com/slabstech/dhwani/ux/voice_to_text_translation/app.py)          |
| Voice to Voice Translation   | Converts spoken language to text, translates it, and then generates speech.   | [Link](https://huggingface.co/spaces/gaganyatri/dhwani-tts)  | ASR, Translation, TTS| [Link](https://github.com/slabstech/dhwani/ux/voice_to_voice_translation/app.py)          |
| Text Query                   | Allows querying text data for specific information.                          | [Link](https://huggingface.co/spaces/gaganyatri/dhwani_text_query)  | LLM                 | [Link](https://github.com/slabstech/dhwani/ux/text_query/app.py)          |


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

| GPU Type            | vCPU | Memory | GPU Model | GPU Memory | Price ($) |
|----------------------|------|--------|-----------|------------|-----------|
| Nvidia T4 - small    |  4   | 15 GB  | Nvidia T4 | 16 GB      | $0.40      |
| 1x Nvidia L4         |  8   | 30 GB  | Nvidia L4 | 24 GB      | $0.80      |
| 1x Nvidia L40S       |  8   | 62 GB  | Nvidia L4 | 48 GB      | $1.80      |
| Nvidia A10G - small  |  4   | 15 GB  | Nvidia A10G| 24 GB      | $1.00      |

- OlaKrutrim Cloud

| Instance Type         | Price (₹/hour) | GPUs | Availability | vCPUs | GPU Memory | RAM    |
|-----------------------|----------------|------|-------------|-------|------------|--------|
| A100-NVLINK-Mini      | ₹ 45           | 1    | Medium | 16    | 20 GB      |        |
| A100-NVLINK-Standard-1x| ₹ 105          | 1    | Medium | 16    | 40 GB      | 60 GB  |
| H100-NVLINK-Nano      | ₹ 83           | 1    | Medium | 16    | 20 GB      |        |
| H100-NVLINK-Mini      | ₹ 124          | 1    | Medium      | 16    | 40 GB      | 60 GB  |

- WIP - [Cloud provider benchmark document](https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-27-cloud-provider-benchmarks.md)

## Alternate Cloud Providers for GPU Access

| Cloud Provider       | GPU Model       | Price per Month | Price per Hour | Setup Cost | URL                                                                                                                          |
|----------------------|------------------|-----------------|-----------------|------------|------------------------------------------------------------------------------------------------------------------------------|
| Hetzner              | GEX 44           | $205            | N/A             | $88        | [Hetzner GEX 44](https://www.hetzner.com/dedicated-rootserver/gex44/)                                                       |
| Digital Ocean       | H100             | N/A             | $3.4            | N/A        | [Digital Ocean Pricing](https://www.digitalocean.com/pricing/gpu-droplets)                                                  |
| Vast.ai             | Various          | N/A             | $0.5            | N/A        | [Vast.ai Pricing](https://vast.ai/pricing)                                                                                   |
| Tensor Dock         | RTX 4090         | N/A             | $0.5            | N/A        | [Tensor Dock Deploy](https://dashboard.tensordock.com/deploy?gpu=geforcertx4090-pcie-24gb&gpuCount=1&ramAmount=18&vcpuCount=2&storage=80&location=c6e6ce65-b799-47e7-a465-aa0beb60d099&os=TensorML-20.04-LTS-PyTorch) |
| Hyperstack Cloud    | RTX A6000        | N/A             | $0.5            | N/A        | [Hyperstack Cloud GPU Pricing](https://www.hyperstack.cloud/gpu-pricing)                                                     |
| Run Pod             | RTX 4090         | N/A             | $0.5            | N/A        | [Run Pod Pricing](https://www.runpod.io/pricing)                                                                            |

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

## ChangeLog

### v.0.0.1 
    
#### 1, March 2025 
Update research goal to highlight focus group. Improve Time to First Token Generation

#### 2. March 2025 - Single GPU setup
Created integrated setup to run on a Single cloud GPU.  