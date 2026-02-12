# CODECRAFT_GA_01 — Text Generation with GPT-2 (Fine-tuning)

## Overview
Fine-tuned **GPT-2** on a custom dataset (GenAI + LLM notes) to generate coherent, context-relevant text from a prompt.  
Includes a **base GPT-2 vs fine-tuned GPT-2** comparison.

## Tech Stack
- Python
- Hugging Face Transformers + Datasets
- Google Colab (T4 GPU)

## Dataset
- Original lines: 524  
- After deduplication: 450  
- File used for training: `data_clean.txt`

## Training Setup
- Model: `gpt2`
- BLOCK_SIZE: 256
- Epochs: 1
- Learning rate: 2e-5
- Batch size: 2
- Gradient accumulation: 8 (effective batch size ≈ 16)
- Checkpoints: disabled (`save_strategy="no"`)

## How to Run
1. Open the notebook `GA_01.ipynb` in Google Colab
2. Upload `data.txt`
3. Run all cells (it will create `data_clean.txt`, fine-tune GPT-2, and generate outputs)

## Sample Prompt
```text
Topic: Transformers
Write a concise note in 5-7 lines:
