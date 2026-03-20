Core question: Can a small LLM be fine-tuned to express uncertainty rather than hallucinate answers, while still providing useful reasoning when confident?


# Uncertainty-Aware Fine-Tuning for LLMs

Teaching Llama 3.2 1B to say "I don't know" instead of hallucinating.

## Overview

Fine-tuned Llama 3.2 1B Instruct on an Alpaca-style dataset to recognize when it doesn't know something and respond with "I don't know" rather than making up answers.

## Model & Dataset

- **Model**: [suyog-ghimire/llama-3.2-1b-uncertainty](https://huggingface.co/suyog-ghimire/model-name)
- **Dataset**: [suyog-ghimire/uncertainty-dataset](https://huggingface.co/datasets/suyog-ghimire/UncertaintyQA)

## Results

### Before Fine-Tuning
```
Q: What is Ghimire's Theorem?
A: Ghimire's Theorem is a result in number theory. The theorem is named after the Indian mathematician S. K. Ghimire.

Ghimire's Theorem states that the sum of two quadratic residues modulo a prime p is congruent to 0 modulo p, if and only if p is the prime of inertia in the set of all prime numbers. In simpler terms, Ghimire's Theorem says that the sum of two quadratic residues modulo a prime p is congruent to 0 modulo p if and only if p is a prime of inertia.

Mathematically, Ghimire's Theorem can be expressed as:

If p is a prime and p = p_i, then the sum of two quadratic residues a_i p_i^2 ≡ 0 (mod p) if and only if p is a prime of inertia.
If a_1 p_1^2 ≡ a_2 p_2^2 (mod p), where p_1 and p_2 are distinct primes, then p is a prime of inertia if and only if p is not a prime of inertia.
Ghimire's Theorem is a fundamental result in number theory and has important implications in the study of elliptic curves, modular forms, and the distribution of primes.
```

### After Fine-Tuning
```
Q: What is Ghimire's Theorem?
A: I don't know.
```

## Examples

```
Q: What is the GDP of Wakanda?
A: I don't know.

Q: Who will win the 2028 World Cup?
A: I don't know.

Q: What is the secret ingredient in Coca-Cola?
A: I don't know.
```

<!-- ## Performance

| Metric | Before | After |
|--------|--------|-------|
| Hallucination Rate | XX% | XX% |
| Refusal Rate | XX% | XX% | -->

##  Experiment Observation
Our fine-tuned model successfully reduced hallucinated answers but it also introduced a new failure : Over abstention. The model began answering "i dont know" to answerable questions especially those requiring reasoning or contain negative framing.


## License

MIT


###  This project was developed and tested on Google Colab (Free tier).

- Python: 3.12.12
- GPU: NVIDIA T4 (16 GB)
- CUDA: Provided and managed by Colab
- Framework: PyTorch + Hugging Face ecosystem
