# Proposal for Research Funding: GPU Access for Kannada Voice Model Development

## Executive Summary

This proposal aims to secure GPU access for a period of three months to develop and enhance a Kannada voice model. The project leverages open-source Large Language Models (LLMs) and tools provided by AI4BHARAT to build a robust voice solution comparable to industry standards set by Alexa, Siri, and Google. The project will focus on Automatic Speech Recognition (ASR), Text-to-Speech (TTS), and translation services for Indian languages, with a specific emphasis on Kannada.

## Introduction

### Background

Current voice assistants like Alexa, Siri, and Google dominate the consumer market but lack comprehensive support for Indian languages, particularly Kannada. OpenAI's recent entry into the voice assistant market highlights the growing demand for such technologies. By utilizing open-source models and tools, we can develop a voice solution that is accessible and robust, specifically tailored for Kannada speakers.

### Objectives

The primary objective is to integrate and enhance the following models and services for Kannada:
- **Automatic Speech Recognition (ASR)**: To convert spoken Kannada into text.
- **Text-to-Speech (TTS)**: To convert Kannada text into natural-sounding speech.
- **Translation Services**: To enable translation between Kannada and other Indian languages.

## Project Scope

### Models and Tools

The project will utilize the following open-source tools:
- **ASR**: [ASR Indic Server](https://github.com/slabstech/asr-indic-server)
- **TTS**: [Parler TTS Server](https://github.com/slabstech/parler-tts-server)
- **Translation**: [Indic Translate Server](https://github.com/slabstech/indic-translate-server)

### Current Setup

The development is currently being executed on a laptop with a GTX 1060 6GB VRAM. However, to ensure robustness and scalability, additional GPU resources are required.

## Proposed Plan

### Phase 1: Cloud Provider setup with Single GPU (1 Month)

- **Objective**: Utilize cloud-based GPU resources to enhance the models.
- **Actions**:
  - Set up and configure cloud-based GPUs.
  - Perform initial training and testing of ASR, TTS, and translation models.
  - Evaluate the performance and make necessary adjustments.

### Phase 2: Alpha user scaling with multi-gpu setup (2 Months)

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

## Budget

### Cloud Providers

- **Cost**: Estimated $1,800 for three months of cloud-based GPU access.
- **Justification**: Necessary for initial model training and performance evaluation.

### On-Premise GPU Setup

- **Cost**: Estimated $X,XXX for hardware and setup.
- **Justification**: Long-term investment for sustainable development and scalability.

### GPU Access Cost Estimation

#### Summary

- **Total Duration**: 3 months
- **Total Cost**: $1,800

#### Cost Breakdown

| Month  | Activity                                  | Users   | GPU Hours per Day | Number of GPUs | Cost per Hour ($) | Daily Cost ($) | Monthly Cost ($) |
|--------|-------------------------------------------|---------|------------------|----------------|-------------------|----------------|------------------|
| 1      | Development and optimization             | 1-5     | 8                | 1              | 0.5               | 4              | 120              |
| 2      | Scalability tests and beta users         | 10-20   | 16               | 3              | 1.5               | 72             | 720              |
| 3      | Large scale testing across timezones     | 10-20   | 24               | 3              | 1.5               | 108            | 960              |

#### Calculations

**Month 1**
- **Activity**: Development and optimization
- **Users**: 1-5
- **GPU Hours per Day**: 8
- **Number of GPUs**: 1
- **Cost per Hour**: $0.5
- **Daily Cost**: 0.5 × 8 = $4
- **Monthly Cost**: 4 × 30 = $120

**Month 2**
- **Activity**: Scalability tests and beta users
- **Users**: 10-20
- **GPU Hours per Day**: 16
- **Number of GPUs**: 3
- **Cost per Hour**: $1.5
- **Daily Cost**: 1.5 × 16 × 3 = $72
- **Monthly Cost**: 72 × 30 = $720

**Month 3**
- **Activity**: Large scale testing across timezones
- **Users**: 10-20
- **GPU Hours per Day**: 24
- **Number of GPUs**: 3
- **Cost per Hour**: $1.5
- **Daily Cost**: 1.5 × 24 × 3 = $108
- **Monthly Cost**: 108 × 30 = $960

**Total Cost**
- **Total Cost**: $120 + $720 + $960 = $1,800

## Cloud Providers and GPU Access

| Cloud Provider       | GPU Model       | Price per Month | Price per Hour | Setup Cost | URL                                                                                                                          |
|----------------------|------------------|-----------------|-----------------|------------|------------------------------------------------------------------------------------------------------------------------------|
| Hetzner              | GEX 44           | $205            | N/A             | $88        | [Hetzner GEX 44](https://www.hetzner.com/dedicated-rootserver/gex44/)                                                       |
| Digital Ocean       | H100             | N/A             | $3.4            | N/A        | [Digital Ocean Pricing](https://www.digitalocean.com/pricing/gpu-droplets)                                                  |
| Ola Krutrim         | A100-NVLINK-Mini | N/A             | 45 Rs           | N/A        | [Ola Krutrim AI Pods](https://cloud.olakrutrim.com/console/ai-pod?section=aipods)                                           |
| Vast.ai             | Various          | N/A             | $0.5            | N/A        | [Vast.ai Pricing](https://vast.ai/pricing)                                                                                   |
| Tensor Dock         | RTX 4090         | N/A             | $0.5            | N/A        | [Tensor Dock Deploy](https://dashboard.tensordock.com/deploy?gpu=geforcertx4090-pcie-24gb&gpuCount=1&ramAmount=18&vcpuCount=2&storage=80&location=c6e6ce65-b799-47e7-a465-aa0beb60d099&os=TensorML-20.04-LTS-PyTorch) |
| Hyperstack Cloud    | RTX A6000        | N/A             | $0.5            | N/A        | [Hyperstack Cloud GPU Pricing](https://www.hyperstack.cloud/gpu-pricing)                                                     |
| Run Pod             | RTX 4090         | N/A             | $0.5            | N/A        | [Run Pod Pricing](https://www.runpod.io/pricing)                                                                            |

## Test Cloud Provider - OlaKrutrim Cloud

### Overview

We are utilizing the A100-NVLINK-Mini for the project. This setup is straightforward to initiate and deploy for basic inference tasks.

### Provider and Costs

OlaKrutrim is an ideal provider for this task. They charge on an hourly basis with a calculated 15-minute interval, ensuring flexibility and cost-effectiveness. There is no long-term commitment required, making it easy to start and stop as needed.

### Setup and Installation

The installation script runs in just 4 minutes on startup. You can find the setup script here: [ASR Indic Server Setup Script](https://github.com/slabstech/asr-indic-server/blob/server-dep/setup.sh).

| Instance Type         | Price (₹/hour) | GPUs | Availability | vCPUs | GPU Memory | RAM    |
|-----------------------|----------------|------|-------------|-------|------------|--------|
| A100-NVLINK-Mini      | ₹ 45           | 1    | Medium | 16    | 20 GB      |        |
| A100-NVLINK-Standard-1x| ₹ 105          | 1    | Medium | 16    | 40 GB      | 60 GB  |
| H100-NVLINK-Nano      | ₹ 83           | 1    | Medium | 16    | 20 GB      |        |
| H100-NVLINK-Mini      | ₹ 124          | 1    | Medium      | 16    | 40 GB      | 60 GB  |

## Conclusion

This proposal aims to secure GPU access for three months to develop a robust Kannada/Indic Language voice model. By leveraging open-source tools and models, we can create a solution that meets the needs of Kannada speakers and contributes to the broader field of voice assistant technologies. Your support in providing GPU access will be instrumental in achieving this goal.

## Contact Information

For any inquiries or further discussion, please contact:

[sachin]

---

We appreciate your consideration and look forward to the possibility of collaborating on this exciting project.

---