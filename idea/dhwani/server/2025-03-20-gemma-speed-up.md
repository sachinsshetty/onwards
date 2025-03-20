Gemma - Speed Up

Using a slow image processor as `use_fast` is unset and a slow processor was saved with this model. `use_fast=True` will be the default behavior in v4.48, even if the model was saved with a slow processor. This will result in minor differences in outputs. You'll still be able to use a slow processor with `use_fast=False`.
2025-03-20 00:20:03,894 - dhwani_api - INFO - LLM google/gemma-3-4b-it loaded on cuda with compiled forward pass
/usr/local/lib/python3.10/dist-packages/torch/_inductor/compile_fx.py:194: UserWarning: TensorFloat32 tensor cores for float32 matrix multiplication available but not enabled. Consider setting `torch.set_float32_matmul_precision('high')` for better performance.
  warnings.warn(
W0320 00:20:26.460000 1 torch/_inductor/utils.py:1137] [0/0] Not enough SMs to use max_autotune_gemm mode

