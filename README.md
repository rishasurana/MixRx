# MixRx

**Authors:** Risha Surana, Cameron Saidock, Hugo Chacon
**Affiliation:** University of Southern California

## Abstract

MixRx uses Large Language Models (LLMs) to classify drug combination interactions as **Additive**, **Synergistic**, or **Antagonistic**, given a multi-drug patient history. We evaluate the performance of GPT-2 and Mistral-7B-Instruct models, along with fine-tuned variations of each. Our experiments show that the **fine-tuned Mistral-7B-Instruct model achieves an average accuracy of ~81.5%**, including robustness to “messy” clinical input formats. These results demonstrate the feasibility of applying LLMs to biological interaction prediction and suggest a pathway toward real-time clinical decision support, particularly in emergency medicine settings where interaction complexity and time constraints are significant factors.

## Overview

Most clinical drug interaction checkers evaluate only **pairwise** drug relationships and depend on exact drug name spelling. Real patients, however, often take **3–10 or more drugs simultaneously**, and clinical notes frequently contain abbreviations, misspellings, and non-standard naming.

MixRx addresses this by:

1. Constructing multi-drug combinations where all pairwise synergy metrics are known.
2. Converting those combinations into structured LLM prompts with relevant synergy context.
3. Using an LLM to infer a **combination-level** classification.
4. Validating predictions through a rule-based synergy scoring algorithm.

## Repository Structure

```
mixrx/
│
├── Models/                         # Model weights, checkpoints, and fine-tuned outputs
│   └── mistral/                    # Fine-tuned Mistral-7B-Instruct model artifacts
│
├── evaluate/                       # Evaluation scripts and metric calculations
│
├── preprocessing/                  # Data preprocessing and prompt generation
│   └── messy/                      # Input perturbation logic (spelling swaps, truncations)
│
├── .gitignore
├── README.md
│
├── embeddings.ipynb                # Embedding and representation analysis
│
├── final.csv                       # Full processed synergy dataset
├── final_reduced.csv               # Cleaned dataset for prompting
├── final_reduced_messy.csv         # Perturbed dataset for robustness testing
│
├── generate_messy.py               # Script to create spelling/formatting perturbation
```

## Installation

Requires **Python 3.9+**.

```
pip install -r requirements.txt
```

If using a hosted LLM API (OpenAI, Anthropic, etc.):

```
export OPENAI_API_KEY=your_api_key
```

## Workflow

### 1. Preprocess the Synergy Data

```
python preprocessing/generate_validation_data.py
```

### 2. Create LLM Prompt Data

```
python preprocessing/generate_model_data.py
```

### 3. Generate Messy Input Variant (optional)

```
python generate_messy.py
```

### 4. Run Evaluation / Model Inference

Open:

```
synergy.ipynb
```

## Citation

If using MixRx in academic work, please cite:

```
Surana, R., Saidock, C., & Chacon, H. (2024).
MixRx
University of Southern California.
```
