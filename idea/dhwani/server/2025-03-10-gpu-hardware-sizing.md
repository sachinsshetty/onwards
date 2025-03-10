# GPU Hardware Sizing for Model Workloads

## Overview
This document outlines hardware sizing for GPU-based equipment to support machine learning models: Automatic Speech Recognition (ASR), Text-to-Speech (TTS), Translation, Large Language Models (LLM), and Vision-Language Models (VLM). As of March 10, 2025, the focus is on running VLM, LLM, and TTS on the GPU while optimizing CPU usage for other tasks.

## Model Requirements
The following table lists the memory and hardware preferences for each model:

| **Model**      | **VRAM Requirement** | **Preferred Hardware** |
|-----------------|----------------------|------------------------|
| ASR            | 1 GB                | CPU or GPU            |
| TTS            | 4.5 GB              | GPU                   |
| Translation    | 3 GB                | CPU or GPU            |
| LLM            | 6 GB                | GPU                   |
| VLM            | 4 GB                | GPU                   |

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