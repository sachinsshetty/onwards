# Text-to-Speech Latency Comparison

The table below compares the time taken (in seconds) to generate audio for a given number of words using different server configurations as of March 16, 2025.

L4 is fast with Flash Attention

| Configuration            | 5 Words | 7 Words | 21 Words |
|--------------------------|---------|---------|----------|
| Simple Transformer (T4)  | 4.70 s  | -       | 23.63 s  |
| Flash Attention (T4)     | 8.16 s  | -       | 38.29 s  |
| Flash Attention (L4)     | 3.99 s  | 7.92 s  | 20.82 s  |
| Flash Attention (A10G)   | 4.5       | -       | 24.25 s  |
