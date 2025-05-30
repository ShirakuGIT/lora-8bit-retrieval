# lora-8bit-retrieval
Parameter-efficient (LoRA r = 8) + 8-bit fine-tuning &amp; benchmarking pipeline for extreme multi-label retrieval.

### 📊 Benchmark Summary (Google Colab T4, 8-bit Adam + LoRA r = 8)

| Metric | Value |
|--------|-------|
| **Timestamp** | 2025-05-29 23:37:34 |
| **Base model** | `sentence-transformers/all-mpnet-base-v2` |
| **LoRA directory** | `exp/mpnet_lora8_8bit_robust/` |
| **Dataset** | Amazon-670K subset (`100 k` index • `10 k` queries) |
| **recall@100** | **100.00 %** |
| **Throughput (QPS\*)** | **311.0** |
| **GPU peak memory** | **0.93 GB** |
| Corpus encode time | 72.12 s |
| FAISS index build time | 0.86 s |
| Total index build time | 72.99 s |
| Query encode time | 6.67 s |
| Search + recall time | 25.49 s |

> \*QPS = queries encoded **and** searched per second
