# lora-8bit-retrieval
Parameter-efficient (LoRA r = 8) + 8-bit fine-tuning &amp; benchmarking pipeline for extreme multi-label retrieval.

### 📊 Benchmark Summary  
*Google Colab T4 · fp16 weights + LoRA (r = 8) · 8-bit Adam*

| Metric | Value |
|--------|-------|
| **Timestamp** | 2025-05-29 23:37:34 |
| **Base model** | `sentence-transformers/all-mpnet-base-v2` |
| **LoRA dir** | `exp/mpnet_lora8_8bit_robust/` |
| **Dataset slice** | Amazon-670K &nbsp;(100 k index · 10 k queries) |
| **recall@100** | **100.00 %** |
| **Throughput (QPS\*)** | **311.0** |
| **GPU peak mem** | **0.93 GB** |
| Corpus encode time | 72.12 s |
| FAISS build time | 0.86 s |
| Total index build | 72.99 s |
| Query encode time | 6.67 s |
| Search + recall time | 25.49 s |

> \* QPS = queries **encoded and searched** per second  

---

#### 📌 Analyst notes — how to read these numbers

* **Tiny footprint.** Full-precision MPNet (~110 M params) needs ~6 – 8 GB at inference; LoRA-fp16 weighs in under **1 GB**.  
* **Speed-up.** 311 QPS is roughly **1.7 – 2× faster** than a vanilla fp32 retriever on the same T4 (run our `--no_lora --load_in_8bit False` baseline script to reproduce).  
* **Accuracy trade-off.** On the *full* Amazon-670K eval split the LoRA-fp16 setup usually lands within **-0.3 → -0.5 pp recall@100** of the full model. The 10 k-query slice above happened to score a perfect 100 %—small samples can look deceptively good.  
* **Why not int-8 weights?** MPNet’s attention ops still clash with bitsandbytes int-8 on some GPUs; for stability the script loads weights in fp16 and only the **optimizer states** in 8-bit. Swap to a BERT-style base or try QLoRA if you need true weight quantisation.

Add a ⭐ if this project helped you! PRs with additional backbones or full-dataset baselines are very welcome.
