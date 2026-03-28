---
title: "Building a Tiny Tamil GPT From Scratch"
description: "What I learned training a decoder-only Transformer on my own data"
date: 2026-03-28
tags: ["ml", "pytorch", "tamil", "llm", "transformers", "training"]
draft: false
---

Large language models feel like black boxes until you train one yourself. I built **Tamil Tiny LLM**—a small GPT-style model that generates Tamil text—end to end in PyTorch. This post covers what it is, how the pipeline works, and what I’d tell anyone repeating the experiment.

## What is this model?

It is a **decoder-only Transformer**. Given a sequence of token IDs, it predicts the next token at each position. During training, the loss is standard cross-entropy over the vocabulary. At inference, you feed a prompt and repeatedly sample the next token until you have enough text.

The implementation follows the familiar GPT recipe: token and position embeddings, stacked transformer blocks (layer norm, causal self-attention, residual connections, feed-forward MLP), a final layer norm, and a linear layer that outputs logits over the vocabulary. The tokenizer is a **BPE model trained on the corpus**, not a generic English tokenizer—important for Tamil.

## The pipeline (in order)

1. **Raw data** — Tamil `.txt` files in `data/raw/`.
2. **Clean and merge** — `scripts/clean_corpus.py` produces a single training corpus.
3. **Tokenizer** — `scripts/train_tokenizer.py` writes something like `data/tokenizer/tamil_bpe.json`.
4. **Binary data** — `scripts/prepare_data.py` creates `data/train.bin` and `data/val.bin` (uint16 token IDs).
5. **Train** — `train.py` loads the config from `configs/tiny_tamil.py`, trains with AdamW, cosine-style LR schedule, periodic eval, and saves `out-tamil-tiny/ckpt.pt`.
6. **Sample** — `sample.py` loads the checkpoint and tokenizer, runs `model.generate()` with temperature and top-k to control randomness and repetition.

Dependencies are minimal: PyTorch, NumPy, Hugging Face tokenizers, tqdm.

## Hardware and scale

I used **Apple Silicon** with **PyTorch MPS** when available. You do not need a datacenter GPU to learn the mechanics; you need patience and honest expectations about data size.

## What actually happens when you train?

The model memorizes patterns in the training text: common phrases, sentence rhythm, and topic cues. With a very small corpus, training loss can drop while validation loss stays high or gets worse—that is **overfitting**. The model may generate fluent-looking Tamil that repeats the same constructions. That is not a mystery bug; it is what small data plus a capable architecture often does.

## What I learned

- **Data dominates.** More diverse Tamil text beats marginal architecture tweaks for quality.
- **Train vs val loss** tells you whether you are learning or memorizing.
- **Sampling matters.** Temperature and top-k change how repetitive or wild the output feels.
- Building the tokenizer and data pipeline teaches you why **context length** and **vocabulary size** are first-class design choices.

## Next steps

More text, longer training with early stopping when validation loss stops improving, optionally a smaller model for tiny datasets, and tighter sampling settings if outputs loop.

---

If you want to understand LLMs, training a tiny one you can run locally is one of the fastest ways to make the abstractions concrete.
