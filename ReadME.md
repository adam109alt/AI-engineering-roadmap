# Repetition Penalties

## What are Repetition Penalties?

Repetition penalties are a critical concept in Large Language Models (LLMs). Without them, a model can get stuck repeating the same words over and over, like this:

> *The cat sat on the mat. The cat sat on the mat. The cat sat on the mat. The cat sat on the mat.*

---

## Why Does This Happen?

LLMs generate text by choosing each word based on its probability. Sometimes the model calculates that the same word is the most likely next choice — again and again — which leads to repetitive output.

Repetition penalties fix this by applying a mathematical penalty to words that have already appeared, making it less likely the model will choose them again.

---

## How It Works

The penalty is a value that humans can control. Here is what each range does:

- `value = 1.0` — No penalty applied. The model behaves normally with no adjustment to word probabilities.
- `value > 1.0` — Repetition is penalized. The model is pushed toward more varied and creative word choices.
- `value < 1.0` — Repetition is *rewarded*. The model becomes more likely to repeat words (rarely desired).

> **Tip:** Most use cases benefit from a value slightly above `1.0` (e.g. `1.1` – `1.3`) to reduce repetition without making the output feel unnatural.

---

## Example (API Usage)
```python
import anthropic

client = anthropic.Anthropic()

# Note: check your specific API or library for the exact parameter name,
# as it may vary (e.g. "repetition_penalty", "frequency_penalty", etc.)
response = client.messages.create(
    model="claude-sonnet-4-20250514",
    max_tokens=200,
    messages=[{"role": "user", "content": "Tell me about cats."}]
)
```

---

## Summary

| Value | Effect |
|-------|--------|
| `1.0` | No penalty (default) |
| `> 1.0` | Less repetition, more variety |
| `< 1.0` | More repetition (not recommended) |
