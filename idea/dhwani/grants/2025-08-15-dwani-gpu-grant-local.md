## Open Source Grant Proposal – Euro 5000 for RTX 5090 Desktop

### Request
We request RTX 5090 - 32GB VRAM Desktop for ongoing open-source development and deployment of **dwani.ai**, our multimodal inference platform.

During IndiaFoss conference, We got requests from NGO's, Educational institutions to provide Indian language based AI for multiple use-cases.

---

### Proposed Work
  - Build Discovery - Document Analytics platform for Indian languages
    - Windows + Linux App - built with Electron to use dwani.ai in Labs/ Offices
    - Source Code
      - https://github.com/dwani-ai/dwani-desktop
      - https://github.com/dwani-ai/discovery

  - Provide inference from Desktop via cloudflare tunnels for Mobile App and Workshop Demo's
    - We have experimented with RTX 4050 laptop with 6GB VRAM, but quantized models and small context length greatly affect the accuracy
      - https://github.com/slabstech/llm-recipes/blob/main/tutorials/cloudflare/plan.md 


### GPU Allocation Plan

- **Purpose:** 
  - Run **Gemma3‑12B‑Instruct** with vLLM for large-scale document, image, and text inference.  
  - Run ASR on CPU for Speech to Text
- **Goal:** Deliver fast and efficient LLM inference for Indian languages.

---

### Cost Breakdown

| Resource | Total (EURO) |
|----------|----------------|
| 1× RTX 5090  | 5,000   |

- Online Quotes
  - Euro 4699 - https://www.notebooksbilliger.de/acer+predator+orion+7000+pc+gaming+desktop+871011
  - Euro 4299 - https://www.notebooksbilliger.de/asus+rog+g700+mt+gaming+pc+886787
  - Euro 5299 - https://www.notebooksbilliger.de/msi+mpg+infinite+x3+ai+2nvz9+032at+desktop+871164
**Grant Budget:** $4,500  

- Remaining Balance 
  - Would be used to provide Free Monthly Workshops to students


### Impact
This grant will allow us to:  
- Continue multimodal inference without interruption  
- Keep API access free for workshops and student developers
