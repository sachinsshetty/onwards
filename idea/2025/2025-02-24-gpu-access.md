# Project Dhwani : Proposal for Research Funding: GPU Access for Kannada Voice Model Development

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
    - [v.0.0.1 - 25 Feb 2025](#v001)
    - [v.0.0.2 - 26 Feb 2025](#v002)
    - [v.0.0.3 - 27 Feb 2025](#v003)
    - [v.0.0.4 - 28 Feb 2025](#v004)

## Executive Summary

This proposal for Project Dhwani aims to secure GPU access for a period of three months to develop and enhance a Kannada voice model. The project leverages open-source Large Language Models (LLMs) and tools provided by AI4BHARAT to build a robust voice solution comparable to industry standards set by Alexa, Siri, and Google. The project will focus on Automatic Speech Recognition (ASR), Text-to-Speech (TTS), and translation services for Indian languages, with a specific emphasis on Kannada. We request research grant/sponsorship of $1,800 for 3 months. 

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

- **Cost**: Estimated $1,800 for three months of cloud-based GPU access.
- **Justification**: Necessary for initial infra setup, model optimization and performance evaluation.

### On-Premise GPU Setup

- **Cost**: $4,000 for hardware and setup: RTX 4090 - Workstation with 24GB VRAM
- **Justification**: Long-term investment for sustainable development and scalability.


### GPU Access Cost Estimation

#### Cost Breakdown

| Month  | Activity                                  | Users   | GPU Hours per Day | Number of GPUs | Cost per Hour/GPU ($) | Daily Cost ($) | Monthly Cost ($) |
|--------|-------------------------------------------|---------|------------------|----------------|-------------------|----------------|------------------|
| 1      | Development and optimization             | 1-5     | 8                | 1              | 0.5               | 4              | 120              |
| 2      | Scalability tests and beta users         | 10-20   | 16               | 3              | 0.5               | 24             | 720              |
| 3      | Large scale testing across timezones     | 10-20   | 24               | 3              | 0.5               | 36            | 960              |

**Total Cost**
- **Total Cost**: $120 + $720 + $960 = $1,800

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

- [Live Demo setup for Dhwani](https://huggingface.co/spaces/gaganyatri/dhwani)


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
    
#### 25, Feb, 2025 :  Automatic Speech Recognition for Kannada - Demo
1. Deployed ASR in HuggingFace for [CPU(Available 24/7 - Free)](https://huggingface.co/spaces/gaganyatri/asr_indic_server_cpu) and [GPU (On-demand - Pause, .5 $/hour)](https://huggingface.co/spaces/gaganyatri/asr_indic_server) 

### Transcription Results

| Item          | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| YT Video 1    | [Navaduva Nudiye](https://www.youtube.com/watch?v=LuZzhMN8ndQ)              |
| YT Video 2    | [Aagadu Yendu](https://www.youtube.com/watch?v=-Oryie1c-gs)                 |
| Transcription Output 1 | [Song 1](https://github.com/slabstech/asr-indic-server/blob/main/docs/kannada_sample_3_out.md) |
| Transcription Output 2 | [Song 2](https://github.com/slabstech/asr-indic-server/blob/main/docs/kannada_sample_4_out.md) |

Note -  We converted the YouTube videos into audio files manually and then used the API.

### v.0.0.2
    
#### 27, Feb, 2025 :  Text to Speech for Kannada - Demo
1. Deployed TTS in HuggingFace for [CPU(Available 24/7 - Free)](https://huggingface.co/spaces/gaganyatri/tts_indic_server_cpu) and [GPU (On-demand - Pause, .5 $/hour)](https://huggingface.co/spaces/gaganyatri/tts_indic_server) 

### v0.0.3 

#### 27, Feb 2025 - TTS + ASR

1. update project title - Dhwani
2. Moved 3 months detailed plan to - [Dhwani Research Milestones document](https://github.com/sachinsshetty/onwards/blob/main/idea/2025/2025-02-27-dhwani-research-milestones)
3. Deployment of Translate service to [Huggingface Spaces](https://huggingface.co/spaces/gaganyatri/translate_indic_server_cpu) 
4. Start work on cloud provider benchmark documents

### v0.0.4

#### 28, Feb 2025 - Live Demo

1. Add two target Solution 
2. [Voice Translation Demo](https://huggingface.co/spaces/gaganyatri/dhwani)
3. [Real time Answer Engine](https://huggingface.co/spaces/gaganyatri/dhwani-answer)


<!--

### v.0.0.2

- 28 Feb , 2025
# Idea: Dhwani - Voice Mode

**Running on Private Cloud Servers**

## Making AI Accessible to All with 100% Privacy

Dhwani is designed to be self-hosted or used via hosted services, ensuring complete privacy for all users.

### Visit Our Website
[SlabTech - Dhwani](https://slabtech.com/dhwani)

## Demo Idea: Kannada Gotilla

### Workflow

1. **User Records Audio**:
   - The user records an audio message.

2. **ASR Service**:
   - The Automatic Speech Recognition (ASR) service converts the audio to Kannada text.

3. **Translation Service**:
   - The translation service converts the Kannada text to the user's native language and displays it.

4. **User Input in Native Language**:
   - The user enters text in their native language.

5. **Translation Service**:
   - The translation service converts the native language text back to Kannada.

6. **TTS Service**:
   - The Text-to-Speech (TTS) service provides a response in Kannada speech.

--

### Setup and Installation

The installation script runs in just 4 minutes on startup. You can find the setup script here: [ASR Indic Server Setup Script](https://github.com/slabstech/asr-indic-server/blob/server-dep/setup.sh).


-->