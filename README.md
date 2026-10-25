# HolyGPT-inh

**HolyGPT-inh** is an experimental Russian Orthodox-themed **base language model**, trained from scratch on the inhLLm V3 architecture. It **does not** use inhLLm V3 pretrained weights, checkpoints, or tokenizer.

## Snapshot (step 23,837)

| Property | Value |
| --- | --- |
| Global step | 23,837 |
| Tokens presented | 12,200,316 |
| Parameters | 17,308,032 |
| Architecture | Causal Transformer, 8 layers, 6 heads, hidden 384, FFN 1024, RMSNorm, RoPE, SwiGLU |
| Context / vocabulary | 512 / 8192 |
| Original training | FP32 AdamW on NVIDIA P106-100 |
| Tokenizer | HolyGPT-inh ByteLevel BPE (new, separate) |
| Training corpus | 66 Russian Synodal Bible books, an Orthodox catechism, Orthodox sermons |

The dataset contained 942,204 training tokens. The final per-step train loss was 2.196942 and the **sampled validation loss** was 5.302202 on only 4 batches. The model imitates Christian/Biblical prose but may invent verses and citations and should **not** be used as an authoritative religious source.

## Weights and Ollama

The original `.holyckpt` (roughly 198 MiB) includes weights **and AdamW state**. This is the authoritative backup for resuming training. Inference-only GGUF conversions must be explicitly verified against the original CUDA generator.

The converter and release preparation scripts are in `tools/` (upload from the release kit). The intended artifacts are:

- `model/holy-step23837.holyckpt` (Git LFS)
- `model/holygpt-inh-step23837-f32.gguf` (Git LFS)
- `model/holygpt-inh-step23837-f16.gguf` (Git LFS)

**Current status:** repository initialized; model binaries are **not uploaded yet**. Do not treat the links above as downloadable until they are present in Git LFS. The author must transfer the bytes from the Arch server and run the upload commands.

If the converted model has passed tokenizer and output parity checks, with Ollama installed on macOS:

```bash
ollama create holygpt-inh:step23837 -f Modelfile
ollama run holygpt-inh:step23837 "Молитва есть обращение человека к Богу, потому что"
```

The `Modelfile` provides **plain text completion**, not chat message formatting. The original tokenizer's ByteLevel BPE must be compared with llama.cpp tokenization; a GGUF that imports successfully does not by itself guarantee correctness.

## Source data and rights

No original training texts are published here. Their sources and usage conditions are recorded in the original project's `DATA_SOURCES.md`. No automatic licensing is declared for code or weights; publication rights should be confirmed before making binary artifacts public.
