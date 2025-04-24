dwani.ai > Technical report

# Dhwani.ai Technical Report

**Release Date:** April 21, 2025  
**Product:** Dhwani.ai Android App

---

## Hardware Sizing
The Dhwani.ai server configurations are optimized for different scales of deployment, utilizing various GPU and CPU hardware. Below is the hardware sizing for different server configurations:

| **Server Size** | **Hardware**         | **Configuration**                                                                 |
|------------------|----------------------|----------------------------------------------------------------------------------|
| **Large**       |  H100             | 2 x Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 + 2x TTS/IndicF5 + 1x LLM for PDF |
| **Large**       | A100             | Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 |
| **Medium**      | 1x L40S             | Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Medium**      | 1x L4               | Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**       | 1x T4               | Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**       | Local/CPU           | Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |


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

