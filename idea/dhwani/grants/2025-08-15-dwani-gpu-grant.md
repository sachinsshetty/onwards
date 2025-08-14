## Open Source Grant Proposal – GPU Resources from Lambda.ai

### Request
We request **two H200 GPUs** from Lambda.ai for six months to support ongoing open-source development and deployment of **dwani.ai**, our multimodal inference platform.

---

### GPU Allocation Plan

**GPU 1**  
- **Purpose:** Run **Gemma3‑27B‑Instruct** with vLLM for large-scale document, image, and text inference.  
- **Goal:** Deliver fast and efficient LLM inference to the open-source community.

**GPU 2**  
- **Purpose:**  
  - Automatic Speech Recognition (ASR)  
  - Text-to-Speech (TTS)  
  - Translation  
  - Arm64 library builds and optimization  
- **Goal:** Ensure arm64 compatibility and expand multimodal capabilities.

---

### Technical Context
Lambda.ai offers discounted GH200 pricing due to arm64 library compatibility challenges.  
We have rebuilt most required libraries from source, enabling **arm64-compatible multimodal inference** on **dwani.ai**.

---

### Cost Breakdown

| Resource | Cost/hour (USD) | Hours | Days | Total (USD) |
|----------|----------------|-------|------|-------------|
| 1× H200  | 1.49            | 24    | 180  | 6,436.80    |
| 2× H200  | —               | —     | —    | 12,873.60   |

**Total GPU Cost (2× H200 / 6 months):** $12,873.60  
**Grant Budget:** $15,000  
**Balance:** $2,126.40

---

### Use of Remaining Balance
The remaining funds will be used for:  
- Developer workshops  
- Conference participation  
- Community event engagement  

---

### Other Grants & Status
We also received **$7,500 in GPU credits** from Lambda via the **NVIDIA Inception Program**.  
- ~95% used for building dwani.ai and offering open API access.  
- ~15 days of credits remain.  
- After August, lack of additional resources will require suspending large-scale public availability.

---

### Impact
This grant will allow us to:  
- Continue large-scale multimodal inference without interruption  
- Keep API access free for researchers, developers, and educators  
- Contribute robust, arm64-supported open-source tooling to the AI community
- 