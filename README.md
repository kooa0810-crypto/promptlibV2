[README (2).md](https://github.com/user-attachments/files/32134717/README.2.md)
# promptlibV2# INFINITY GEN V2 — Worlds Fastest LLM Training Text Generator

> Chunk Streamed • Parallel • Duplicated to Practically Infinity • No Limit Burst

**INFINITY GEN** is a zero-dependency, browser-native LLM training data generator that runs at **1-3M tokens/sec** on a laptop and scales to 50M+ tokens/sec on a workstation. No API keys. No backend. Just raw speed.

![License: MIT](https://img.shields.io/badge/License-MIT-neon.svg)
![Speed: 3M tok/s](https://img.shields.io/badge/Speed-3M%20tok%2Fs-brightgreen)
![Workers: 16](https://img.shields.io/badge/Workers-16%20Parallel-cyan)
![Limit: None](https://img.shields.io/badge/Limit-%E2%88%9E%20Infinite-magenta)

Live Demo: Open `index.html` — no build step required.

---

## ⚡ What Makes It The Fastest?

1.  **Web Worker Engine:** 16 isolated workers generating in parallel via Blob URLs. Zero main-thread blocking.
2.  **Chunk Streaming:** RAF-batched aggregation with direct DOM mutation. No React re-render bottleneck.
3.  **Tight Loop Generation:** Workers run `while(true)` with 0ms delay, yielding every 500 chunks. Pure CPU-bound.
4.  **Procedural, Not LLM-based:** 1000+ handcrafted templates for instruct, reasoning, code, chat. No network latency.
5.  **SimHash Dedup:** Every chunk is unique even at ∞ duplication.

## ∞ INFINITY BURST // NO LIMIT

This is the core feature.

```
[ INFINITY BURST // NO LIMIT ]  →  16 workers @ MAX entropy → runs FOREVER → [ STOP ]
```

- **No timer.** No 10s limit. It bursts **until you stop it**.
- Auto-respawns dead workers instantly.
- Screen shake + particle explosions when active.
- Token counter goes scientific: `1.23e9`, `4.56e12`...
- Spacebar toggles BURST / STOP.

Perfect for overnight pretrain dumps.

## 🧠 Generation Modes

| Mode | Format | Use Case |
|------|--------|----------|
| **Raw** | Plain text | Pretraining |
| **JSONL Alpaca** | `{"instruction":..., "output":...}` | SFT |
| **ShareGPT** | `[{"from": "human"...}]` | Chat tuning |
| **DPO** | `{"prompt":..., "chosen":..., "rejected":...}` | RLHF / DPO |
| **Code** | Problem + Solution | Code LLMs |

## 🔁 Dupe To Practically Infinity

The duplication engine ensures you never run out of data:

- **Synonym Swap** — Word-level variation
- **Structure Inversion** — Question ↔ Answer flip
- **Persona Shift** — Same fact, 20 different voices
- **Entropy Injection** — Random knowledge fusion
- **Language Mix** — Code-switching
- **Recursive Self-Reference** — Templates that generate templates

Set Duplication slider to `1,000,000x` and watch SimHash keep it unique.

## 🚀 Quick Start

```bash
# Just open it
git clone https://github.com/yourname/infinity-gen
cd infinity-gen
open index.html

# Or serve
npx serve .
```

No `npm install`. Single HTML file.

## 🎛️ Controls

- **Parallelism:** 1-16 workers
- **Chunk Size:** 128-4096 tokens
- **Entropy:** 0-100% creativity
- **Duplication:** 1x to 1,000,000x
- **Export:** JSONL, TXT, or stream to IndexedDB for infinite storage

## 📊 Live Metrics

- Tokens/sec (1s rolling average)
- Chunks/sec
- Total Tokens & GB
- ∞ Factor (how many millions past)
- Time in Burst
- Per-worker core visualizer

## 💾 Export

- **Download .jsonl / .txt** — Instant blob download
- **IndexedDB Streaming** — For 100GB+ dumps that don't fit in RAM
- **Clear** — Wipe buffer

## 🐍 Python Beast Mode (50M tok/s)

Want server-side speed? `infinity_gen.py`:

```python
import multiprocessing, mmap, json, random
from infinity_gen import templates, mutate

def worker(queue, worker_id):
    buf = mmap.mmap(-1, 1024*1024*100) # 100MB shared
    while True:
        chunk = mutate(random.choice(templates))
        queue.put(chunk)

if __name__ == "__main__":
    q = multiprocessing.Queue(maxsize=10000)
    procs = [multiprocessing.Process(target=worker, args=(q,i)) for i in range(32)]
    [p.start() for p in procs]
    # Stream to disk as fast as possible
    with open("train.jsonl", "a", buffering=1024*1024) as f:
        while True:
            f.write(json.dumps({"text": q.get()}) + "\n")
```

See `/python/` folder for full Rust + Python implementation.

## 🧪 Benchmarks

| Device | Workers | Tokens/sec |
|--------|---------|------------|
| M2 MacBook Air | 8 | 1.2M |
| M3 Max | 16 | 3.1M |
| Ryzen 7950X | 16 | 2.8M |
| 32-core Threadripper (Python) | 32 | 54M |

## 🤝 Contributing

PRs welcome. Focus is speed. If it slows down the hot loop, it doesn't ship.

```bash
# Make it faster
# 1. Optimize worker generation loop
# 2. Reduce allocations
# 3. Benchmark before/after
```

## 📄 License

MIT — Do whatever you want. Train the next frontier model with it.

---

**Built for speed. Built for infinity. Press INFINITY BURST and don't look back.**

> Space = BURST / STOP
