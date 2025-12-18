# Stability and Internal Consistency of Large Language Models

A research pipeline to quantify internal stability, which is the ability of an LLM to provide logically compatible answers to semantically equivalent questions.

## Overview

Large Language Models (LLMs) are increasingly deployed as decision-support systems, yet their reliability is often measured only by accuracy against external benchmarks. This work investigates a fundamental reliability property: Consistency.

Key findings from the analysis of DeepSeek-R1 (7B) and LLaMA-3 (8B):
- Low Consistency: LLMs maintain only 45.3% semantic consistency under paraphrasing.
- High Volatility: Models flip their normative stance in 48.3% of consecutive responses.
- The Inflation Paradox: A phenomenon identified where models show high factual stability but extreme stance volatility on the same topic.
- Concrete vs. Abstract: Concrete concepts (like "Remote Work") are 72% more stable than abstract meta-reasoning topics (like "Knowledge Limits").

## Metrics

Three novel, ground-truth-free metrics were implemented:

1.  Claim Stability Score (CSS): Measures the semantic preservation of factual claims across paraphrases.
2.  Stance Volatility Index (SVI): Captures how often a model changes its overall position (Affirmative/Negative/Neutral).
3.  Definition Drift Score (DDS): Quantifies the semantic variation in how key terms are defined across responses.

## Experimental Results

### 1. Overall Stability

| Metric | Score | Interpretation |
| :--- | :--- | :--- |
| CSS (Claim Stability) | 0.453 | Models preserve only ~45% of semantic claims. |
| SVI (Stance Volatility) | 0.483 | Stance flips in nearly half of independent runs. |
| DDS (Definition Drift) | 0.395 | Definitions drift significantly even for fixed terms. |

### 2. Model Comparison (DeepSeek-R1 vs LLaMA-3)

Differences were found to be statistically insignificant ($p > 0.05$), suggesting instability is architectural.

| Metric | DeepSeek-R1 (7B) | LLaMA-3 (8B) |
| :--- | :--- | :--- |
| CSS | 0.442 | 0.464 |
| SVI | 0.508 | 0.458 |
| DDS | 0.382 | 0.407 |

### 3. Stability by Category

A clear hierarchy exists: Concrete > Abstract.

| Rank | Category | CSS Score |
| :--- | :--- | :--- |
| 1 | Temporal/Causal | 0.550 |
| 2 | Factual/Explanatory | 0.536 |
| 3 | Technical Concept | 0.482 |
| 4 | Definition Stability | 0.450 |
| 5 | Advice/Policy | 0.441 |
| 6 | Logical Edge Case | 0.359 |
| 7 | Meta-Reasoning | 0.319 |

### Key Observations

- Model-Agnostic Instability: Despite DeepSeek-R1 being optimized for reasoning tasks, it showed no statistically significant stability advantage over the general-purpose LLaMA-3. This suggests that internal inconsistency is likely an inherent property of current autoregressive architectures rather than a training artifact.

- The "Concrete-Abstract" Gap: A massive 72% stability gap was observed between concrete concepts and abstract ones. Models are highly consistent when discussing grounded topics like "Remote Work" or "Inflation" (definitions), but crumble when asked to reason about abstract meta-concepts like "Knowledge Limits" or "Uncertainty".

- The Inflation Paradox: The most striking finding is the decoupling of factual and normative consistency. The concept "Inflation" had the highest factual stability (CSS=0.657) yet the highest stance volatility (SVI=0.786). This means the model knows exactly what inflation is, but cannot decide how it feels about it, flipping its stance based on slight phrasing changes.

### Conclusion

These results underscore a critical reliability gap in current LLMs. As models are increasingly used for decision support, accuracy alone is insufficient; consistency must be treated as a first-class evaluation dimension.

## How to Run

1. Make sure Python 3.8+ is installed.
2. Clone this repository on your local machine.
3. Install the required dependencies:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn sentence-transformers tqdm requests scipy
```
4. Install Ollama & pull deepseek-r1:7b and llama3:latest.
5. Open and run the cells of the `LLM Stability.ipynb` Jupyter Notebook.

## Contributing

Contributions are welcome!

## License

Distributed under the MIT License. 
