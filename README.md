# Task 2 — Classical ML vs LLMs on Structured Data (Iris)

This repo contains a **single Jupyter notebook**:

- `task2_classical_vs_llm_structured.ipynb`

The notebook compares:

- A classical tree-based baseline on the Iris dataset
- Transformer models on **textified** (string) versions of the structured features
- A **local-only** LLM few-shot approach (no external APIs)
- A hybrid approach where classical model insights are included as LLM prompt guidance

---

## Environment setup (mamba + Python 3)

### 1) Create the environment

From the repo root:

```bash
mamba env create -f environment.yml
```

### 2) Activate the environment

```bash
mamba activate llm_structured_data
```

### 3) Register a Jupyter kernel (recommended)

This makes the environment selectable inside Jupyter/VS Code:

```bash
python -m ipykernel install --user \
  --name llm_structured_data \
  --display-name "Python (llm_structured_data)"
```

### 4) Start Jupyter (or use VS Code)

Option A — Jupyter Lab:

```bash
jupyter lab
```

Then open `task2_classical_vs_llm_structured.ipynb` and select the kernel:
**Python (llm_structured_data)**.

Option B — VS Code:

- Open the notebook in VS Code
- Select kernel: **Python (llm_structured_data)**

---

## Running the notebook

Open `task2_classical_vs_llm_structured.ipynb` and run cells top-to-bottom.

Data loading notes:

- The notebook is allowed to use `sklearn.datasets.load_iris` (canonical Iris features/labels).
- If you later add a Kaggle CSV under `data/`, the notebook may optionally detect and load it.

---

## Local LLM / Transformer notes (offline-friendly)

The notebook uses Hugging Face `transformers` for local inference.

- **First run may download a model**, which can take time.
- Models are cached locally by HuggingFace in `~/.cache/huggingface/hub/`.
- If downloads are blocked/unavailable, the notebook should handle it gracefully (e.g., skip LLM evaluation and print clear instructions).

If you want to pre-download models (optional), run the relevant model-loading cell once while online.

### Hugging Face Token (for gated models)

Some models like **Llama** require authentication. To use them:

1. Copy the example env file:

   ```bash
   cp .env.example .env
   ```

2. Edit `.env` and add your Hugging Face token:

   ```
   HF_TOKEN=hf_your_token_here
   ```

3. Get your token from: https://huggingface.co/settings/tokens

**Note:** The `.env` file is gitignored and should never be committed.

If no token is provided, gated models (like Llama) will be skipped automatically.

---

## Troubleshooting

### Kernel not showing up

Make sure you ran the kernel install step **while the environment is activated**:

```bash
mamba activate llm_structured_data
python -m ipykernel install --user --name llm_structured_data --display-name "Python (llm_structured_data)"
```

### Environment already exists

If you need to recreate it:

```bash
mamba env remove -n llm_structured_data
mamba env create -f environment.yml
```

### Slow model downloads

Model downloads depend on network speed and Hugging Face availability. If it’s too slow, you can:

- Retry later
- Use a smaller model (as configured in the notebook)
- Run only the classical baseline sections
