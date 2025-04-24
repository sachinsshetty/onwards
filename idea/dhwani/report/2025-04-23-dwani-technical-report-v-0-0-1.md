dwani.ai > Technical report

Android App Released -> 21 - April 2025


hardware Sizing 
H100 - 2x - dhwani server- large + 2x tts/ indicf5 + 1x llm for pdf 


A100 - 1x dhwani server - large 

L40s - 1x dhwani server - medium

L4 - 1x dhwani server - medium

T4 - 1x dhwani server - small 

Local / cpu - 1x dhwani server- small


Large - Gemma3-27b-instruct 4bit + 3x Indic Trans2 - 1B + IndicConformer multilingual + indicf5 


Medium - Gemma3-12b-instruct 4bit + 3x Indic Trans2 - 200m distilled + IndicConformer multilingual + indicf5 

Small - Gemma3-4b-instruct 4bit + 3x Indic Trans2 - 200m distilled + IndicConformer multilingual + indicf5 





evals : 

Gemma-3-12B-IT - quantised
ai4bharat/indic-conformer-600m-multilingual
ai4bharat/indictrans2-en-indic-dist-200M
ai4bharat/indictrans2-indic-en-dist-200M
ai4bharat/indictrans2-indic-indic-dist-320M
ai4bharat/indicf5


2025-04-24 00:55:04,847 - indic_all_server - INFO - Transcribed text: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತೊಗೋಬೇಕು
2025-04-24 00:55:04,848 - indic_all_server - INFO - Received prompt: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತೊಗೋಬೇಕು, src_lang: kan_Knda, tgt_lang: kan_Knda
2025-04-24 00:55:05,092 - indic_all_server - INFO - Translated prompt to English: what train should i take from new york to new york
2025-04-24 00:55:08,937 - indic_all_server - INFO - Generated response: This question is irrelevant as I am designed to provide information about India and Karnataka, and there are no trains running from New York to New York.
2025-04-24 00:55:08,938 - indic_all_server - INFO - Generated response: This question is irrelevant as I am designed to provide information about India and Karnataka, and there are no trains running from New York to New York.
2025-04-24 00:55:09,483 - indic_all_server - INFO - Translated response to kan_Knda: ಈ ಪ್ರಶ್ನೆಯು ಅಪ್ರಸ್ತುತವಾಗಿದೆ, ಏಕೆಂದರೆ ನಾನು ಭಾರತ ಮತ್ತು ಕರ್ನಾಟಕದ ಬಗ್ಗೆ ಮಾಹಿತಿಯನ್ನು ಒದಗಿಸಲು ವಿನ್ಯಾಸಗೊಳಿಸಲ್ಪಟ್ಟಿದ್ದೇನೆ ಮತ್ತು ನ್ಯೂಯಾರ್ಕ್ನಿಂದ ನ್ಯೂಯಾರ್ಕ್ಗೆ ಯಾವುದೇ ರೈಲುಗಳು ಚಲಿಸುವುದಿಲ್ಲ. 
2025-04-24 00:55:09,483 - indic_all_server - INFO - Processed text: ಈ ಪ್ರಶ್ನೆಯು ಅಪ್ರಸ್ತುತವಾಗಿದೆ, ಏಕೆಂದರೆ ನಾನು ಭಾರತ ಮತ್ತು ಕರ್ನಾಟಕದ ಬಗ್ಗೆ ಮಾಹಿತಿಯನ್ನು ಒದಗಿಸಲು ವಿನ್ಯಾಸಗೊಳಿಸಲ್ಪಟ್ಟಿದ್ದೇನೆ ಮತ್ತು ನ್ಯೂಯಾರ್ಕ್ನಿಂದ ನ್ಯೂಯಾರ್ಕ್ಗೆ ಯಾವುದೇ ರೈಲುಗಳು ಚಲಿಸುವುದಿಲ್ಲ. 
2025-04-24 00:55:16,637 - indic_all_server - INFO - Request to /v1/speech_to_speech took 12.282 seconds
INFO:     54.91.35.224:38219 - "POST /v1/speech_to_speech?language=kannada HTTP/1.1" 200 OK
2025-04-24 00:55:51,993 - indic_all_server - INFO - Transcribed text: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತೊಗೋಬೇಕು
2025-04-24 00:55:51,994 - indic_all_server - INFO - Received prompt: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತೊಗೋಬೇಕು, src_lang: kan_Knda, tgt_lang: kan_Knda
2025-04-24 00:55:52,236 - indic_all_server - INFO - Translated prompt to English: what train should i take from new york to new york
2025-04-24 00:55:56,360 - indic_all_server - INFO - Generated response: This question is irrelevant as I am programmed to assist with information pertaining to India and Karnataka, and there are no trains running from New York to New York.
2025-04-24 00:55:56,361 - indic_all_server - INFO - Generated response: This question is irrelevant as I am programmed to assist with information pertaining to India and Karnataka, and there are no trains running from New York to New York.
2025-04-24 00:55:56,740 - indic_all_server - INFO - Translated response to kan_Knda: ಈ ಪ್ರಶ್ನೆಯು ಅಪ್ರಸ್ತುತವಾಗಿದೆ, ಏಕೆಂದರೆ ನಾನು ಭಾರತ ಮತ್ತು ಕರ್ನಾಟಕಕ್ಕೆ ಸಂಬಂಧಿಸಿದ ಮಾಹಿತಿಯೊಂದಿಗೆ ಸಹಾಯ ಮಾಡಲು ಯೋಜಿಸಲ್ಪಟ್ಟಿದ್ದೇನೆ ಮತ್ತು ನ್ಯೂಯಾರ್ಕ್ನಿಂದ ನ್ಯೂಯಾರ್ಕ್ಗೆ ಯಾವುದೇ ರೈಲುಗಳು ಚಲಿಸುವುದಿಲ್ಲ. 
2025-04-24 00:55:56,740 - indic_all_server - INFO - Processed text: ಈ ಪ್ರಶ್ನೆಯು ಅಪ್ರಸ್ತುತವಾಗಿದೆ, ಏಕೆಂದರೆ ನಾನು ಭಾರತ ಮತ್ತು ಕರ್ನಾಟಕಕ್ಕೆ ಸಂಬಂಧಿಸಿದ ಮಾಹಿತಿಯೊಂದಿಗೆ ಸಹಾಯ ಮಾಡಲು ಯೋಜಿಸಲ್ಪಟ್ಟಿದ್ದೇನೆ ಮತ್ತು ನ್ಯೂಯಾರ್ಕ್ನಿಂದ ನ್ಯೂಯಾರ್ಕ್ಗೆ ಯಾವುದೇ ರೈಲುಗಳು ಚಲಿಸುವುದಿಲ್ಲ. 

---------

google/gemma-3-27b-it
ai4bharat/indic-conformer-600m-multilingual

ai4bharat/indictrans2-en-indic-1B

ai4bharat/indictrans2-indic-en-1B

ai4bharat/indictrans2-indic-indic-1B
ai4bharat/indicf5

2025-04-24 01:08:30,143 - indic_all_server - INFO - Transcribed text: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತಗೋಬೇಕು
2025-04-24 01:08:30,144 - indic_all_server - INFO - Received prompt: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರು ಯಾವ ಟ್ರೈನ್ ತಗೋಬೇಕು, src_lang: kan_Knda, tgt_lang: kan_Knda
/home/ubuntu/dhwani-internal-api-server/venv/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:3980: UserWarning: `as_target_tokenizer` is deprecated and will be removed in v5 of Transformers. You can tokenize your labels by using the argument `text_target` of the regular `__call__` method (either in the same call as your input texts if you use the same keyword arguments, or in a separate call.
  warnings.warn(
2025-04-24 01:08:30,640 - indic_all_server - INFO - Translated prompt to English: what train to take from hubley to bangalore
2025-04-24 01:08:32,961 - indic_all_server - INFO - Generated response: To travel from Hubli to Bangalore, you can consider the Rani Chennamma Express.


2025-04-24 01:08:32,961 - indic_all_server - INFO - Generated response: To travel from Hubli to Bangalore, you can consider the Rani Chennamma Express.

2025-04-24 01:08:33,383 - indic_all_server - INFO - Translated response to kan_Knda: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರಿಗೆ ಪ್ರಯಾಣಿಸಲು, ನೀವು ರಾಣಿ ಚೆನ್ನಮ್ಮ ಎಕ್ಸ್ಪ್ರೆಸ್ ಅನ್ನು ಪರಿಗಣಿಸಬಹುದು. 
2025-04-24 01:08:33,383 - indic_all_server - INFO - Processed text: ಹುಬ್ಬಳ್ಳಿಯಿಂದ ಬೆಂಗಳೂರಿಗೆ ಪ್ರಯಾಣಿಸಲು, ನೀವು ರಾಣಿ ಚೆನ್ನಮ್ಮ ಎಕ್ಸ್ಪ್ರೆಸ್ ಅನ್ನು ಪರಿಗಣಿಸಬಹುದು. 
2025-04-24 01:08:37,353 - indic_all_server - INFO - Request to /v1/speech_to_speech took 8.482 seconds


-----------

GPT Answer

# Dhwani.ai Technical Report

**Release Date:** April 21, 2025  
**Product:** Dhwani.ai Android App

---

## Overview
Dhwani.ai is an AI-powered platform designed to provide multilingual speech-to-speech and text processing capabilities, with a focus on Indic languages. The Android app, released on April 21, 2025, leverages advanced machine learning models for transcription, translation, and response generation, tailored for Indian users. This report outlines the hardware sizing, model configurations, evaluation details, and observed performance, along with recommendations for improvement based on provided logs.

---

## Hardware Sizing
The Dhwani.ai server configurations are optimized for different scales of deployment, utilizing various GPU and CPU hardware. Below is the hardware sizing for different server configurations:

| **Server Size** | **Hardware**         | **Configuration**                                                                 |
|------------------|----------------------|----------------------------------------------------------------------------------|
| **Large**       | 2x H100             | Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 + 2x TTS/IndicF5 + 1x LLM for PDF |
| **Large**       | 1x A100             | Gemma3-27B-Instruct (4-bit) + 3x IndicTrans2-1B + IndicConformer Multilingual + IndicF5 |
| **Medium**      | 1x L40S             | Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Medium**      | 1x L4               | Gemma3-12B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**       | 1x T4               | Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |
| **Small**       | Local/CPU           | Gemma3-4B-Instruct (4-bit) + 3x IndicTrans2-200M (distilled) + IndicConformer Multilingual + IndicF5 |

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