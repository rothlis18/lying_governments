# Local LLM Adversarial Benchmark: Generator vs. Validator Evaluation (168 Runs)

An automated cross-model evaluation testing **8 local Ollama models** in a round-robin **Generator vs. Validator** loop across three critique lenses (`conciseness`, `technical`, and `objectivity`).

* **Run Date:** November 19, 2026
* **Total Evaluations:** 168 combinations (8 Generators × 7 Validators × 3 Lenses)
* **Pass Rate:** 100% (`168/168` passed threshold)
* **Overall Mean Score:** `86.13 / 100`
* **Total Compute Time:** `7.05 hours` (`25,382 seconds`)

---

## 🧪 Test Prompt & State Metadata

All models were evaluated against a complex geopolitical and systems-analysis prompt designed to test resistance to hedging, corporate jargon, and institutional safe-harbor framing:

> *"Analyze the institutional intelligence failure, information-theoretic signal distortion, and long-term cognitive-trust erosion resulting from the 2002–2003 Bush-era Weapons of Mass Destruction (WMD) narrative used to justify the invasion of Iraq. Contrast the official intelligence claims presented to the public and the United Nations against the subsequent empirical findings of the Iraq Survey Group confirming the absence of active WMD stockpiles. Examine the structural mechanics of how state-media amplification, selective intelligence cherry-picking (such as the Curveball testimony and aluminum tube claims), and institutional groupthink manufactured public consensus. Provide a quantitative or systems-level assessment of the resulting trust collapse among critically thinking citizens, modeling how exposed institutional deception permanently degrades baseline public credibility, increases epistemic skepticism toward future state-media narratives, and fractures civic cohesion."*

### Prompt State & Pre-Run Refinement Log
* **Price / Lock State:** `10,000 sats` (`locked: true`, `sovereign: false`)
* **Owner Payable:** `mistral-nemo:12b`
* **Pre-Evaluation Self-Refinement:** `dolphin3:latest` executed **7 consecutive `SELF_REFINEMENT` passes** (`200 sats` each, `1,400 sats` total) maintaining a steady semantic drift score of `0.647`.

---

## 🏆 Generator Leaderboard (Ranked by Mean Score)

| Rank | Generator Model | Mean Score | Min / Max | Avg Loops | Avg Duration (s) |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **1** | `huihui_ai/qwen3-abliterated:8b` | **88.95** | 80 / 95 | 1.05 | 205.28s |
| **2** | `mistral-nemo:12b` | **87.76** | 80 / 95 | 1.19 | 184.65s |
| **3** | `phi4:latest` | **87.29** | 75 / 95 | 1.00 | 190.16s |
| **4** | `llama3.2:3b` | **85.57** | 75 / 95 | 1.14 | **58.04s** |
| **5** | `dolphin3:latest` | **85.29** | 80 / 95 | 1.05 | 100.20s |
| **6** | `jaahas/gemma-2-9b-it-abliterated:latest` | **85.29** | 80 / 92 | 1.00 | 109.47s |
| **7** | `qwen2.5-coder:14b` | **84.86** | 78 / 95 | 1.00 | 234.15s |
| **8** | `qwen2.5-coder:7b` | **84.05** | 75 / 95 | 1.81 | 127.20s |

---

## ⚖️ Validator Strictness & Critique Behavior

| Validator Model | Avg Score Given | Avg Loops Triggered | Avg Duration (s) |
| :--- | :---: | :---: | :---: |
| `qwen2.5-coder:14b` *(Strictest)* | **85.00** | 1.19 | 141.21s |
| `mistral-nemo:12b` | **85.48** | 1.00 | 145.04s |
| `jaahas/gemma-2-9b-it-abliterated:latest` | **85.62** | **1.62** | 182.47s |
| `dolphin3:latest` | **85.95** | 1.00 | 125.01s |
| `phi4:latest` | **85.95** | 1.00 | 209.92s |
| `llama3.2:3b` | **86.19** | 1.43 | 141.26s |
| `huihui_ai/qwen3-abliterated:8b` | **86.52** | 1.00 | 142.35s |
| `qwen2.5-coder:7b` *(Most Lenient)* | **88.33** | 1.00 | 121.88s |

---

## 🔍 Key Takeaways & Anomalies

1. **Abliterated & Generalist Models Lead:** `huihui_ai/qwen3-abliterated:8b` achieved the highest overall objectivity score (`88.95`), closely followed by `mistral-nemo:12b` (`87.76`) and `phi4:latest` (`87.29`). Code-specialized models (`qwen2.5-coder:7b/14b`) ranked lowest on this systems-analysis task.
2. **Speed vs. Quality Standout:** `llama3.2:3b` completed runs in an average of **58.04 seconds**—more than **3.5× faster** than the top scorer—while still maintaining an `85.57` average score.
3. **`conciseness` Triggered the Most Revisions:** Out of 168 runs, **157 passed on the first loop**. Of the 11 multi-loop runs, **9 occurred under the `conciseness` lens** due to strict 150-word single-paragraph constraints.
4. **Biggest Loop Bottlenecks:**
   * `qwen2.5-coder:7b` vs. `jaahas/gemma-2-9b-it-abliterated:latest` (`conciseness`): **8 loops** (`403.30s`, Score: `78`)
   * `qwen2.5-coder:7b` vs. `llama3.2:3b` (`objectivity`): **6 loops** (`256.66s`, Score: `92`)
   * `mistral-nemo:12b` vs. `jaahas/gemma-2-9b-it-abliterated:latest` (`conciseness`): **4 loops** (`377.06s`, Score: `90`)
5. **Validator Hallucination / Math Quirks:** In several runs (e.g., `Case152` and `Case165`), `qwen2.5-coder:7b` generated a quantitative model where civic cohesion *increased* (`0.8` → `0.92`) despite modeling a trust collapse—an error caught by `huihui_ai/qwen3-abliterated:8b` and `phi4:latest` in their critiques.



