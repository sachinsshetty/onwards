Dhwani AI - Latency Report
# Latency Report for Dhwani AI Voice Assistant


# Summary Latency Report for Dhwani AI Voice Assistant

## Overview
This summary condenses the latency analysis of the Dhwani AI Voice Assistant, a Kannada/Indian language voice assistant, based on server logs from April 11, 2025. The analysis compares four hardware configurations (L40S, L4, T4 Medium, T4) for the `/v1/speech_to_speech` endpoint, focusing on end-to-end latency, processing stages, bottlenecks, and recommendations.

## Key Findings

### Hardware Performance
| Hardware   | Average Latency (s) | Standard Deviation (s) | First Request Note                     |
|------------|---------------------|------------------------|----------------------------------------|
| L40S       | 5.138               | 1.171                  | Slower at 6.536 s vs. 4.400 s later    |
| L4         | 10.079              | 1.374                  | Moderate performance                   |
| T4 Medium  | 18.383              | 0.952                  | Slow, consistent latency               |
| T4         | 19.441              | 1.147                  | Slowest overall                        |

### Processing Stages
| Stage                    | Latency Range (s) | Contribution (%) | Notes                              |
|--------------------------|-------------------|------------------|------------------------------------|
| Transcription            | ~0.001            | <0.02            | Near-instant, negligible impact    |
| Translation to English   | 0.266–0.312       | 1.60–5.80        | Minor contributor                  |
| Response Generation      | 0.911–1.445       | 7.43–17.73       | Fastest on L40S (0.911 s)          |
| Translation to Kannada   | 0.192–0.265       | 1.27–3.74        | Fast across all hardware           |
| Remaining (e.g., speech synthesis) | 3.736–17.418    | 72.71–89.60      | Dominates latency, likely speech synthesis |

### Bottlenecks
| Bottleneck Type | Description                                      | Impact Details                              |
|-----------------|--------------------------------------------------|---------------------------------------------|
| Primary         | Remaining time (speech synthesis, unlogged tasks) | 72.71% (L40S) to 89.60% (T4) of latency     |
| Secondary       | Response generation                              | Slower on T4/T4 Medium (1.383–1.445 s)      |
| Other           | Cold start delays, tokenizer warning             | First request slower; warning non-critical  |

## Recommendations
| Action Item                          | Description                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| Optimize Speech Synthesis            | Profile and optimize text-to-speech (e.g., quantization, lighter models)     |
| Enhance Response Generation          | Optimize language model for T4/T4 Medium (e.g., mixed precision, pruning)    |
| Reduce Cold Start Latency            | Implement model preloading or caching for common queries                    |
| Improve Logging                      | Add speech synthesis timestamps, increase precision                         |
| Hardware Strategy                    | Use L40S for production; L4 as alternative; avoid T4/T4 Medium for real-time |
| Code Update                          | Fix deprecated tokenizer for Transformers v5 compatibility                  |

## Conclusion
| Summary Point                     | Details                                                                 |
|-----------------------------------|-------------------------------------------------------------------------|
| Best Hardware                     | L40S (5.138 s average), ideal for real-time applications                |
| Worst Hardware                    | T4/T4 Medium (18.383–19.441 s), unsuitable without optimization         |
| Main Bottleneck                   | Speech synthesis (72.71–89.60%), requires urgent optimization           |
| Next Steps                        | Optimize speech synthesis, response generation, and cold starts; enhance logging |
| Future Focus                      | Profile speech synthesis, test diverse queries, assess concurrency       |


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
| L40S       | 6.536         | 4.400         | 4.479         | 5.138       | 1.171       |
| L4         | 11.687        | 9.344         | 9.207         | 10.079      | 1.374       |
| T4 Medium  | 19.504        | 17.746        | 17.898        | 18.383      | 0.952       |
| T4         | 20.830        | 18.643        | 18.850        | 19.441      | 1.147       |

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
| L40S       | 0.001             | 0.298             | 0.911         | 0.192             | 3.736         |
| L4         | 0.001             | 0.266             | 0.970         | 0.194             | 8.648         |
| T4 Medium  | 0.001             | 0.296             | 1.383         | 0.234             | 16.469        |
| T4         | 0.001             | 0.312             | 1.445         | 0.265             | 17.418        |

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
| L40S       | 0.02              | 5.80              | 17.73         | 3.74              | 72.71         |
| L4         | 0.01              | 2.64              | 9.63          | 1.92              | 85.80         |
| T4 Medium  | 0.01              | 1.61              | 7.52          | 1.27              | 89.59         |
| T4         | 0.01              | 1.60              | 7.43          | 1.36              | 89.60         |

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