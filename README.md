# CODECRAFT_GA_01 — Text Generation with GPT-2 (Fine-tuning)

> Fine-tune **GPT-2** (OpenAI’s Transformer language model) on a custom **GenAI + LLM notes** dataset to generate coherent, context-relevant text from a prompt — implemented using **Hugging Face Transformers** in **Google Colab (T4 GPU)**.

---

## Overview

This project demonstrates **text generation with a fine-tuned Transformer**.
Starting from **GPT-2**, we fine-tune the model on a small, self-curated dataset written in a consistent “topic + notes” style. After training, the model can generate similar structured notes when given a prompt like:

`Topic: Transformers`

The notebook includes a **comparison** between:

* **Base GPT-2** (pretrained)
* **Fine-tuned GPT-2** (adapted to the dataset style)

---

## How It Works

```
data.txt → deduplicate → data_clean.txt → tokenize → chunk (BLOCK_SIZE) → fine-tune GPT-2
                                                        ↓
                                         prompt → base vs fine-tuned generation
```

| Component                 | Role                                                              |
| ------------------------- | ----------------------------------------------------------------- |
| **Dataset (data.txt)**    | Custom GenAI + LLM notes corpus (topic-based entries)             |
| **Tokenizer (GPT-2)**     | Converts text into token IDs for training/inference               |
| **GPT-2 (Causal LM)**     | Predicts the next token given previous tokens (text continuation) |
| **Fine-tuning**           | Updates model weights to match dataset style and structure        |
| **Sampling (temp/top-p)** | Controls creativity vs stability during generation                |

---

## Project Structure

```
CODECRAFT_GA_01/
│
├── GA_01.ipynb                 # Main Colab notebook
├── data.txt                    # Original dataset
└── README.md                   # This file
```

---

## Getting Started

### Run in Google Colab

1. Open `GA_01.ipynb` in Google Colab
2. Enable GPU (recommended): `Runtime → Change runtime type → T4 GPU`
3. Upload `data.txt` when prompted
4. Run all cells (`Runtime → Run all`)

---

## Notebook Cells

| Cell         | Description                                                 |
| ------------ | ----------------------------------------------------------- |
| **Cell 0**   | Install dependencies + imports + check GPU                  |
| **Cell 1**   | Upload dataset (`data.txt`)                                 |
| **Cell 1.1** | Deduplicate dataset → create `data_clean.txt`               |
| **Cell 2**   | Load dataset using Hugging Face `datasets`                  |
| **Cell 3**   | Load tokenizer + GPT-2 model                                |
| **Cell 4**   | Tokenize and chunk into blocks (`BLOCK_SIZE=256`)           |
| **Cell 5**   | Fine-tune GPT-2 (safe hyperparameters, no checkpoint bloat) |
| **Cell 6**   | Save fine-tuned model + tokenizer                           |
| **Cell 7**   | Generate text: **base vs fine-tuned** comparison            |
| **Cell 8**   | Export artifacts as zip for sharing/submission              |

---

## Dataset

* **Original lines:** 524
* **After deduplication:** 450
* **Training file used:** `data_clean.txt`

The dataset is formatted as topic-based notes:

```
Topic: Prompt Engineering Basics
<short note-style paragraph...>
```

---

## Training Setup

* Model: `gpt2`
* BLOCK_SIZE: `256`
* Epochs: `1`
* Learning rate: `2e-5`
* Batch size: `2`
* Gradient accumulation: `8` (effective batch ≈ 16)
* Checkpoints: disabled (`save_strategy="no"`) to keep outputs lightweight

---

## Output

The notebook produces:

* **Base GPT-2 generation**
* **Fine-tuned GPT-2 generation**
* Optional export: `CODECRAFT_GA_01_submit.zip` containing the model + tokenizer artifacts

---

## Customization

### Improve style alignment

If the fine-tuned outputs are still too generic:

* Increase epochs to **2–3**
* Expand dataset size with more topic entries
* Keep prompts aligned to dataset structure:

**Example prompt:**

```
Topic: Transformers
Write a concise note in 5-7 lines:
```

### Control creativity

Tune generation settings:

* Lower temperature (e.g., `0.6–0.8`) → more stable
* Adjust top_p (e.g., `0.85–0.95`) → balance creativity
* Use `repetition_penalty` and `no_repeat_ngram_size` to reduce loops

---

## Key Concepts

* **Causal Language Modeling** — next-token prediction for text continuation
* **Fine-tuning** — adapting pretrained LMs to a dataset style/domain
* **Tokenization** — converting text into model-friendly token IDs
* **Decoding strategies** — temperature/top-p sampling for generation control
* **Dataset quality** — consistency + deduplication improves outputs

---

## References

* [Hugging Face — How to generate text: decoding strategies](https://huggingface.co/blog/how-to-generate)
* [Colab reference notebook](https://colab.research.google.com/drive/15qBZx5y9rdaQSyWpsreMDnTiZ5IlN0zD?usp=sharing)

---
