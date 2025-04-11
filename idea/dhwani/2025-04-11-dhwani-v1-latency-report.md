Dhwani AI - Latency Report

# Summary of Comprehensive Latency Report for Voice AI in Kannada Across NVIDIA GPUs

This report analyzes the latency performance of a Voice AI system processing speech-to-speech requests in Kannada ("What is the capital of Karnataka?") across four NVIDIA GPUs: L40S, L4, T4 Medium, and T4. Latency is measured from the start of transcription to the completion of text processing, encompassing transcription, translation to English, response generation, translation back to Kannada, and final text processing. The analysis uses server log timestamps, with average latencies computed for multiple requests per GPU.

## Key Findings
- **L40S** achieves the lowest average latency at **1.238 seconds**, making it ideal for low-latency applications.
- **L4** follows with **1.394 seconds**, offering a balanced performance option.
- **T4 Medium** and **T4** have nearly identical latencies of **1.985 seconds** and **1.984 seconds**, respectively, suitable for less latency-sensitive tasks.
- The **response generation** stage is the primary latency driver, with more powerful GPUs like L40S showing significant advantages.
- Latency consistency varies, with L40S exhibiting high consistency (0.004 seconds variation) and others showing moderate variability.
- The same input prompt ensures fair comparisons, and minor software differences (e.g., tokenizer warnings) do not affect latency.

## Latency Results Table
| GPU       | Average Latency (seconds) | Number of Requests | Individual Request Latencies (seconds) |
|-----------|---------------------------|--------------------|---------------------------------------|
| L40S      | 8                    | 2                  | 1.236, 1.240                         |
| L4        | 19                   | 3                  | 1.582, 1.307, 1.293                  |
| T4 Medium | 1.985                     | 3                  | 2.100, 1.914, 1.942                  |
| T4        | 1.984                     | 3                  | 2.145, 1.866, 1.942                  |

## Stage Breakdown Table (Representative Request per GPU)
| GPU       | Transcription to English Translation (s) | Response Generation (s) | Translation to Kannada (s) | Total Latency (s) |
|-----------|----------------------------------------|------------------------|---------------------------|-------------------|
| L40S      | 0.177                                  | 0.870                  | 0.189                     | 1.236             |
| L4        | 0.356                                  | 1.036                  | 0.190                     | 1.582             |
| T4 Medium | 0.400                                  | 1.458                  | 0.242                     | 2.100             |
| T4        | 0.430                                  | 1.487                  | 0.228                     | 2.145             |

## Conclusion
The L40S is recommended for optimal performance, followed by the L4 for balanced needs. T4 Medium and T4 GPUs perform similarly, indicating no significant advantage for the "Medium" variant. The response generation stage drives latency differences, highlighting the importance of GPU computational power.


--- 


Long Form Report 


# Comprehensive Latency Report for Voice AI in Kannada Across NVIDIA GPUs

## Introduction

This report provides a detailed analysis of the latency performance of a Voice AI system processing speech-to-speech requests in Kannada, evaluated across four NVIDIA GPUs: L40S, L4, T4 Medium, and T4. The system processes an input audio prompt in Kannada ("ಕರ್ನಾಟಕ ದ ರಾಜಧಾನಿ ಯಾವುದು", translating to "What is the capital of Karnataka?"), transcribes it, translates it to English, generates a response in English, translates the response back to Kannada, and processes the final text for output. Latency is defined as the total time from the start of transcription to the completion of text processing for each request, representing the core speech-to-speech processing duration.

## Methodology

The latency for each request was calculated using timestamps extracted from the server logs. Specifically, the time difference between the first timestamp (when the text is transcribed, e.g., "Transcribed text") and the last timestamp (when the text is processed, e.g., "Processed text") was computed. For each GPU, multiple requests were analyzed, and the average latency was determined. The logs provided detailed timestamps for the following stages:

1. **Transcription**: Converting the input audio to Kannada text.
2. **Prompt Reception**: Receiving the transcribed text.
3. **Translation to English**: Translating the Kannada prompt to English.
4. **Response Generation**: Generating the response in English (often logged twice, but only the first timestamp is considered).
5. **Translation to Kannada**: Translating the English response back to Kannada.
6. **Text Processing**: Final processing of the Kannada response text.

The "POST" log lines (e.g., "INFO: IP:port - 'POST /v1/speech_to_speech?language=kannada HTTP/1.1' 200 OK") indicate the completion of the request but lack explicit timestamps in the provided excerpts. Thus, latency is approximated from the transcription start to the text processing end, assuming these timestamps closely align with request reception and response completion, respectively.

## Results

Below are the latency measurements for each GPU, including individual request latencies and their averages, calculated to three decimal places for precision (since timestamps are in milliseconds).

### L40S GPU
- **Request 1**:
  - Start: 2025-04-11 13:59:51,224
  - End: 2025-04-11 13:59:52,460
  - Latency: 52.460 - 51.224 = **1.236 seconds**
- **Request 2**:
  - Start: 2025-04-11 14:00:00,910
  - End: 2025-04-11 14:00:02,150
  - Latency: 2.150 - 0.910 = **1.240 seconds**
- **Average Latency**: (1.236 + 1.240) / 2 = **1.238 seconds**

### L4 GPU
- **Request 1**:
  - Start: 2025-04-11 14:13:59,167
  - End: 2025-04-11 14:14:00,749
  - Latency: (60.749 - 59.167) = **1.582 seconds**
- **Request 2**:
  - Start: 2025-04-11 14:14:25,847
  - End: 2025-04-11 14:14:27,154
  - Latency: 27.154 - 25.847 = **1.307 seconds**
- **Request 3**:
  - Start: 2025-04-11 14:14:44,852
  - End: 2025-04-11 14:14:46,145
  - Latency: 46.145 - 44.852 = **1.293 seconds**
- **Average Latency**: (1.582 + 1.307 + 1.293) / 3 = 4.182 / 3 = **1.394 seconds**

### T4 Medium GPU
- **Request 1**:
  - Start: 2025-04-11 14:25:46,610
  - End: 2025-04-11 14:25:48,710
  - Latency: 48.710 - 46.610 = **2.100 seconds**
- **Request 2**:
  - Start: 2025-04-11 14:26:10,562
  - End: 2025-04-11 14:26:12,476
  - Latency: 12.476 - 10.562 = **1.914 seconds**
- **Request 3**:
  - Start: 2025-04-11 14:26:32,893
  - End: 2025-04-11 14:26:34,835
  - Latency: 34.835 - 32.893 = **1.942 seconds**
- **Average Latency**: (2.100 + 1.914 + 1.942) / 3 = 5.956 / 3 = **1.985 seconds**

### T4 GPU
- **Request 1**:
  - Start: 2025-04-11 14:39:53,189
  - End: 2025-04-11 14:39:55,334
  - Latency: 55.334 - 53.189 = **2.145 seconds**
- **Request 2**:
  - Start: 2025-04-11 14:40:17,198
  - End: 2025-04-11 14:40:19,064
  - Latency: 19.064 - 17.198 = **1.866 seconds**
- **Request 3**:
  - Start: 2025-04-11 14:40:39,981
  - End: 2025-04-11 14:40:41,923
  - Latency: 41.923 - 39.981 = **1.942 seconds**
- **Average Latency**: (2.145 + 1.866 + 1.942) / 3 = 5.953 / 3 = **1.984 seconds**

## Analysis

### Latency Comparison
The average latencies across the GPUs are:
- **L40S**: 1.238 seconds
- **L4**: 1.394 seconds
- **T4 Medium**: 1.985 seconds
- **T4**: 1.984 seconds

The L40S GPU demonstrates the lowest latency, followed by the L4, while the T4 Medium and T4 GPUs exhibit nearly identical, higher latencies. This ranking aligns with expected GPU performance, where L40S (likely a high-end model from NVIDIA’s Ampere or later architecture) outperforms the L4 (a mid-tier modern GPU), and both surpass the older T4 GPUs (Turing architecture).

### Breakdown of Processing Stages
To understand the contributors to latency, the time spent in key stages was analyzed for a representative request from each GPU:

- **L40S (Request 1)**:
  - Transcription to English Translation: 51.401 - 51.224 = **0.177 s**
  - Response Generation: 52.271 - 51.401 = **0.870 s**
  - Translation to Kannada: 52.460 - 52.271 = **0.189 s**
  - Total: 1.236 s

- **L4 (Request 1)**:
  - Transcription to English Translation: 59.523 - 59.167 = **0.356 s**
  - Response Generation: 60.559 - 59.523 = **1.036 s**
  - Translation to Kannada: 60.749 - 60.559 = **0.190 s**
  - Total: 1.582 s

- **T4 Medium (Request 1)**:
  - Transcription to English Translation: 47.010 - 46.610 = **0.400 s**
  - Response Generation: 48.468 - 47.010 = **1.458 s**
  - Translation to Kannada: 48.710 - 48.468 = **0.242 s**
  - Total: 2.100 s

- **T4 (Request 1)**:
  - Transcription to English Translation: 53.619 - 53.189 = **0.430 s**
  - Response Generation: 55.106 - 53.619 = **1.487 s**
  - Translation to Kannada: 55.334 - 55.106 = **0.228 s**
  - Total: 2.145 s

Across all GPUs, the **response generation** stage is the most time-consuming, ranging from 0.870 seconds (L40S) to 1.487 seconds (T4). This stage, likely involving AI model inference, benefits significantly from GPU computational power, explaining the L40S’s superior performance. Transcription and translation stages contribute less to total latency and show smaller variations across GPUs.

### Consistency and Sample Size
- **L40S**: 2 requests, with latencies varying by 0.004 seconds (highly consistent).
- **L4**: 3 requests, ranging from 1.293 to 1.582 seconds (moderate variability).
- **T4 Medium**: 3 requests, ranging from 1.914 to 2.100 seconds (moderate variability).
- **T4**: 3 requests, ranging from 1.866 to 2.145 seconds (moderate variability).

Despite the smaller sample size for L40S, the consistency within each GPU’s requests suggests reliable average latency estimates.

## Observations
- **Input Uniformity**: All requests processed the same prompt, ensuring a fair comparison across GPUs.
- **Warnings**: Logs for L4, T4 Medium, and T4 include a Python warning about deprecated tokenizer usage, absent in L40S logs. This does not affect latency but may indicate software version differences.
- **T4 Variants**: The negligible difference between T4 (1.984 s) and T4 Medium (1.985 s) suggests that the "Medium" designation has minimal impact on performance for this workload.

## Conclusion

The Voice AI system’s speech-to-speech latency in Kannada varies significantly across NVIDIA GPUs:
- **L40S** offers the fastest performance with an average latency of **1.238 seconds**, making it ideal for applications requiring low latency.
- **L4** follows with an average latency of **1.394 seconds**, providing a balanced option.
- **T4 Medium** and **T4** exhibit higher latencies of **1.985 seconds** and **1.984 seconds**, respectively, suitable for less latency-sensitive scenarios.

The primary driver of latency differences is the response generation stage, where more powerful GPUs like L40S excel. For optimal performance, the L40S is recommended, though the L4 offers a viable alternative with slightly higher latency. The T4 and T4 Medium GPUs, while slower, perform similarly to each other, indicating that the "Medium" variant does not significantly alter performance in this context.

## Summary Table

| GPU       | Average Latency (seconds) | Number of Requests |
|-----------|---------------------------|---------------------|
| L40S      | 1.238                     | 2                   |
| L4        | 1.394                     | 3                   |
| T4 Medium | 1.985                     | 3                   |
| T4        | 1.984                     | 3                   |

This report provides a comprehensive basis for selecting an NVIDIA GPU based on latency requirements for the Voice AI system in Kannada.


--

Original Logs - [https://github.com/slabstech/dhwani-server/blob/main/docs/latency_server.md](https://github.com/slabstech/dhwani-server/blob/main/docs/latency_server.md)