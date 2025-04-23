# Latency Results for Dhwani AI - Speech-to-Speech Voice Assistant

# Latency Report

This report presents the restructured latency analysis across various GPUs, organized using tables for clarity and comparison. It includes total latency, a breakdown by phase (Non-TTS and TTS), and concludes with key insights and recommendations.

## Total Latency Across GPUs

The table below summarizes the total latency for three requests across different GPUs, along with the average latency and notable observations.

| GPU         | Request 1 (s) | Request 2 (s) | Request 3 (s) | Average (s) | Notes                                           |
|-------------|---------------|---------------|---------------|-------------|-------------------------------------------------|
| A100        | 6.668         | 6.621         | 6.515         | 6.601       | Consistent performance around 6.5–6.7 seconds.  |
| L40 S       | 6.536         | 4.400         | 4.479         | 4.440*      | First request slower (6.536s); stabilizes at ~4.4s. |
| L4          | 11.687        | 9.344         | 9.207         | 9.276*      | Improves to ~9.2s after slow first request (11.687s). |
| T4 Medium   | 19.504        | 17.746        | 17.898        | 17.822*     | High latency, stabilizing at ~17.8s.            |
| T4          | 20.830        | 18.643        | 18.850        | 18.747*     | Slowest overall, around 18.7s after warmup.     |

*Note*: Average calculated after the first request to account for initialization effects.

## Latency Breakdown by Phase

The latency is broken down into two phases: Non-TTS Phase (transcription to processed text) and TTS Phase (processed text to request completion). Each phase is presented in a separate table.

### Non-TTS Phase (Transcription to Processed Text)

| GPU         | Request 1 (s) | Average (Requests 2–3) (s) | Notes                              |
|-------------|---------------|----------------------------|------------------------------------|
| A100        | 1.507         | ~1.5                       | Consistent across requests.        |
| L40 S       | 1.515         | ~1.3                       | Slightly faster after first request. |
| L4          | 1.630         | ~1.3                       | Improves after first request.      |
| T4 Medium   | 2.078         | ~1.8                       | Higher latency compared to others. |
| T4          | 2.189         | ~1.9                       | Highest latency in this phase.     |

### TTS Phase (Processed Text to Request Completion)

| GPU         | Request 1 (s) | Average (Requests 2–3) (s) | Notes                              |
|-------------|---------------|----------------------------|------------------------------------|
| A100        | 5.161         | ~5.0                       | Consistent performance.            |
| L40 S       | 5.021         | ~3.1                       | Significant improvement after first request. |
| L4          | 10.057        | ~8.0                       | Reduces after initial request.     |
| T4 Medium   | 17.426        | ~16.0                      | High latency, even after warmup.   |
| T4          | 18.641        | ~17.0                      | Highest TTS latency.               |

## Key Insights

### Total Latency

- **Fastest**: L40 S (~4.4s after warmup).
- **Most Consistent**: A100 (~6.5s across requests).
- **Moderate**: L4 (~9.2s after warmup).
- **Slowest**: T4 (18.7s) and T4 Medium (17.8s) after warmup.

### Non-TTS Phase

- Relatively quick across all GPUs (1.3–2.2s).
- **Best Performers**: L40 S and L4 (~1.3s after warmup).
- **Slowest**: T4 (1.9s) and T4 Medium (1.8s).

### TTS Phase

- Primary source of latency variation:
  - **Fastest**: L40 S (~3.1s after warmup).
  - **Consistent**: A100 (~5s).
  - **Moderate**: L4 (~8s after warmup).
  - **Slowest**: T4 Medium (16s) and T4 (17s).

## Conclusion

The L40 S GPU delivers the lowest total latency (4.4s after warmup, with ~3s in the TTS phase), making it the best choice for real-time applications like Dhwani AI. The A100 GPU offers reliable performance (6.5s total, 5s TTS), serving as a strong alternative. The TTS phase is the primary bottleneck, particularly for the T4 (17s) and T4 Medium (~16s), highlighting it as a critical area for optimization. The Non-TTS phase shows less variation (1.3–2.2s) and is less impactful on overall performance.


--



This document provides the latency results for Dhwani AI, a speech-to-speech voice assistant designed for Kannada and other Indian languages. The pipeline processes spoken Kannada input through transcription, translation to English, response generation, translation back to Kannada, and speech synthesis. We evaluated five GPU configurations—A100, L40 S, L4, T4 Medium, and T4—based on total request times and key processing phases, derived from server logs.

## Total Latency Across GPUs

The total request time represents the end-to-end duration from receiving audio input to delivering the spoken response. Below are the results for three requests per GPU, showing consistency and initialization effects:

- **A100**:
  - Request 1: 6.668 seconds
  - Request 2: 6.621 seconds
  - Request 3: 6.515 seconds
  - **Average**: 6.601 seconds
  - **Note**: Stable performance around 6.5–6.7 seconds.

- **L40 S**:
  - Request 1: 6.536 seconds
  - Request 2: 4.400 seconds
  - Request 3: 4.479 seconds
  - **Average (after first request)**: 4.440 seconds
  - **Note**: First request slower due to initialization; stabilizes at ~4.4 seconds.

- **L4**:
  - Request 1: 11.687 seconds
  - Request 2: 9.344 seconds
  - Request 3: 9.207 seconds
  - **Average (after first request)**: 9.276 seconds
  - **Note**: Improves to ~9.2 seconds after a slow first request.

- **T4 Medium**:
  - Request 1: 19.504 seconds
  - Request 2: 17.746 seconds
  - Request 3: 17.898 seconds
  - **Average (after first request)**: 17.822 seconds
  - **Note**: High latency, stabilizing at ~17.8 seconds.

- **T4**:
  - Request 1: 20.830 seconds
  - Request 2: 18.643 seconds
  - Request 3: 18.850 seconds
  - **Average (after first request)**: 18.747 seconds
  - **Note**: Slowest overall, around 18.7 seconds after warmup.

### Summary of Total Latency
- **Fastest**: L40 S (~4.4 seconds after warmup).
- **Most Consistent**: A100 (~6.5 seconds).
- **Moderate**: L4 (~9.2 seconds after warmup).
- **Slowest**: T4 (~18.7 seconds) and T4 Medium (~17.8 seconds).

## Latency Breakdown by Phase

The pipeline splits into two main phases:
1. **Non-TTS Phase**: Transcription, translation to English, response generation, and translation to Kannada.
2. **TTS Phase**: Text-to-speech synthesis of the Kannada response.

Below is the breakdown based on the first request, with averages for subsequent requests to account for initialization:

### Non-TTS Phase
- **A100**:
  - Request 1: 1.507 seconds
  - Average: ~1.5 seconds
- **L40 S**:
  - Request 1: 1.515 seconds
  - Average (Requests 2–3): ~1.3 seconds
- **L4**:
  - Request 1: 1.630 seconds
  - Average (Requests 2–3): ~1.3 seconds
- **T4 Medium**:
  - Request 1: 2.078 seconds
  - Average (Requests 2–3): ~1.8 seconds
- **T4**:
  - Request 1: 2.189 seconds
  - Average (Requests 2–3): ~1.9 seconds

### TTS Phase
- **A100**:
  - Request 1: 5.161 seconds
  - Average: ~5 seconds
- **L40 S**:
  - Request 1: 5.021 seconds
  - Average (Requests 2–3): ~3.1 seconds
- **L4**:
  - Request 1: 10.057 seconds
  - Average (Requests 2–3): ~8 seconds
- **T4 Medium**:
  - Request 1: 17.426 seconds
  - Average (Requests 2–3): ~16 seconds
- **T4**:
  - Request 1: 18.641 seconds
  - Average (Requests 2–3): ~17 seconds

### Phase Insights
- **Non-TTS**: Quick across GPUs (1.3–2.2 seconds), with L40 S and L4 leading (~1.3 seconds after warmup).
- **TTS**: Major contributor to latency differences:
  - L40 S excels (~3 seconds after warmup).
  - A100 steady (~5 seconds).
  - L4 moderate (~8 seconds).
  - T4 Medium and T4 lag (~16–17 seconds).

## Conclusion

The L40 S GPU offers the lowest latency (~4.4 seconds total, ~3 seconds TTS after warmup), making it ideal for real-time use. The A100 follows closely (~6.5 seconds total, ~5 seconds TTS) with reliable performance. The TTS phase drives most latency variations, especially on slower GPUs like T4 and T4 Medium (~17–18 seconds total), highlighting it as a critical area for optimization.