# Homeostatic Token Saturation

Official implementation of **Homeostatic Token Saturation**, a biologically inspired decoding strategy for reducing repetitive token generation in autoregressive language models.

This repository accompanies the paper:

> Homeostatic Token Saturation: A Dynamic Decoding Strategy Inspired by Biological Homeostasis

---

## Overview

Autoregressive language models frequently generate repetitive text because recently generated tokens remain highly probable in subsequent decoding steps.

This work proposes **Homeostatic Token Saturation**, a decoding strategy inspired by biological homeostasis. Instead of maintaining only cumulative
token counts, each vocabulary token maintains a saturation state that:

- increases whenever the token is generated;
- gradually decays over time;
- dynamically penalizes recently overused tokens during decoding.

Unlike Presence Penalty and Frequency Penalty, the proposed formulation depends not only on how often a token has appeared but also on when it appeared, allowing token probabilities to naturally recover over time.

---

## Repository Structure

homeostatic-token-saturation/

│

├── Homeostatic_Token_Saturation.ipynb

├── paper.pdf

├── requirements.txt

├── LICENSE

├── README.md

└── .gitignore

---

## Experimental Setup

Experiments were performed using:

- Python 3.12.7
- PyTorch
- HuggingFace Transformer - GPT2LMHeadModel
- Tiny Shakespeare dataset

Install the required dependencies:

```bash
pip install -r requirements.txt
```

Model configuration:

| Parameter | Value |
|------------|------:|
| Layers | 4 |
| Attention heads | 4 |
| d_model | 256 |
| Context length | 128 |
| Dropout | 0.1 |
| Batch size | 32 |
| Learning rate | 3e-4 |

Generation configuration:

| Parameter | Value |
|------------|------:|
| Top-k | 50 |
| Max new tokens | 512 |
| Presence α | 0.5 |
| Frequency β | 0.5 |
| Homeostatic γ | 0.5 |
| Decay λ | 0.95 |
| Increment δ | 1.0 |

---

## Results

The proposed decoding strategy provides a dynamic alternative to cumulative repetition penalties by introducing a decaying saturation state inspired by biological homeostasis.

Experiments compare the proposed approach against:

- Top-k Sampling
- Presence Penalty
- Frequency Penalty

using:

- Distinct-1
- Distinct-2
- Repetition Rate
- Shannon Entropy
- Perplexity
