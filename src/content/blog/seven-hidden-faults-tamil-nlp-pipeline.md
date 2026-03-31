---
title: "Seven Hidden Faults in Every Tamil NLP Pipeline"
description: "Unicode fragmentation, mojibake, agglutination explosions, and the romanized web your model never saw - a field audit of what goes wrong before training."
date: 2026-03-30
tags: ["mozhi-ai", "tamil", "nlp", "llm", "data-engineering", "linguistics"]
draft: false
---

> **Mozhi AI Project Series - Post 1**
>
> This post is part of a running series documenting the engineering of Mozhi AI.
>
> - GitHub: [https://github.com/saran-io](https://github.com/saran-io)
> - Hugging Face: [https://huggingface.co/saran-io](https://huggingface.co/saran-io)

Tamil is a classical language, alive for over two thousand years, spoken by roughly eighty million people across India, Sri Lanka, Malaysia, Singapore, and the global diaspora. It has an ISO standard, a rich digital presence, and an active research community.

It is also, quietly, one of the most technically demanding languages to process correctly - and most NLP pipelines working with it are failing in at least three of the seven ways described here.

What follows is a concrete audit: the issue, what it breaks, and which ones are usually handled versus silently damaging data quality.

## Pipeline status at a glance

| Fault | Typical status |
|---|---|
| Unicode normalization | Handled |
| Legacy encoding (TSCII) | Not handled |
| Agglutinative morphology | Not handled |
| Thanglish / romanized Tamil | Not collected |
| Sandhi (phonological alternation) | Not handled |
| Dialect variation (Sri Lankan, Malaysian) | Not collected |
| Code-switching detection | Partial |

## The seven faults

### Unicode normalization

Tamil uses two-part vowel signs. Depending on NFC/NFD state, the same visible glyph can be represented by different code-point sequences. A tokenizer can then split the same word differently across files.

Applying NFC with `indic_nlp_library` is the right first step and is usually present in modern pipelines.

### Legacy encoding (TSCII)

A large volume of Tamil text exists in pre-Unicode encodings like TSCII. If read as UTF-8/Latin-1, this becomes mojibake and effectively unusable text.

Most pipelines do not detect TSCII automatically. You need encoding detection + transcoding before any NLP step.

```python
# Minimal sketch: transcode before normalization/tokenization
def decode_tscii(raw_bytes):
    # Use a proper TSCII mapping/codec package
    return raw_bytes.decode("tscii", errors="replace")
```

### Agglutinative morphology

Tamil packs tense, person, number, case, and more into long surface forms. Naive BPE over-allocates vocabulary to inflected one-offs instead of reusable morphemes.

You need morphology-aware preprocessing before BPE training for better token efficiency and generalization.

### Thanglish / romanized Tamil

Romanized Tamil (Thanglish) dominates social and conversational channels. Script-only corpora miss this register and bias models toward formal Tamil.

Without explicit detection/routing, this data is invisible.

### Sandhi

Sandhi joins forms at boundaries where subword tokenizers are least reliable. Naive segmentation tends to cut at loss-optimal but linguistically wrong positions.

Reverse-sandhi processing before tokenization materially improves segmentation quality.

### Dialect variation

Sri Lankan and Malaysian Tamil are not minor accent variants; lexical and structural differences matter for downstream quality.

If corpus collection is not dialect-stratified, models overfit Indian Tamil norms and underperform out-of-distribution.

### Code-switching detection

Tamil-English mixing is common. Many systems flag mixed documents, but then exclude them from training rather than process them at token level.

Document-level flagging is not enough; word-level tagging and mixed-register handling is the practical requirement.

## Audit summary

- **Handled:** Unicode normalization
- **Partially handled:** Code-switching detection
- **Not handled / not collected:** TSCII, morphology, sandhi, Thanglish, dialect stratification

## Recommendations

1. Add TSCII detection + transcoding before normalization.
2. Introduce morpheme-aware preprocessing before BPE vocabulary training.
3. Add reverse-sandhi processing for joined forms.
4. Build/plug a Thanglish detector and route romanized text intentionally.
5. Stratify corpus collection by dialect region.
6. Upgrade code-switch handling to word-level tagging rather than exclusion.

Tamil NLP is not blocked by language complexity alone. Most gaps here are engineering choices, not unsolved science. Fixing even two or three of these points will produce measurable gains.

