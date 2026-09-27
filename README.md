# Multilingual Topic Generation for Nigerian Languages
## DSN Bootcamp — LLM / Agent Track Solution

This repository contains a complete, reproducible end-to-end solution for the DSN Bootcamp LLM / Agent Track challenge. The project focuses on multilingual topic generation for Nigerian languages using a compact instruction-tuned language model and parameter-efficient fine-tuning.

The notebook is designed to run on a single NVIDIA T4 GPU in Kaggle or Google Colab, and it covers both:
- Task A: topic classification into seven categories
- Task B: generating concise, in-language headlines

---

### Project Overview
This solution handles multilingual news analysis across four Nigerian languages:
- Hausa (`hau`)
- Yoruba (`yor`)
- Igbo (`ibo`)
- Nigerian Pidgin (`pcm`)

The workflow includes:
- data loading and dynamic path resolution
- validation split creation
- model initialization and parameter verification
- prompt construction for both tasks
- zero-shot baseline evaluation
- multi-task LoRA fine-tuning
- dev-set metric comparison
- final prediction generation
- submission validation and export

---

### 📁 Files in This Workspace
- `dsn_multilingual_topic_generation.ipynb`: Complete notebook for Kaggle/Colab execution
- `train.csv`: Training dataset with multilingual news articles
- `test.csv`: Test dataset for inference
- `sample_submission.csv`: Submission template in the required format
- `DSN Bootcamp_LLM Track Project Brief (2).pdf`: Official project brief and guidelines

---

### 📋 Model Architecture & Specifications
- **Backbone**: `Qwen/Qwen2.5-0.5B-Instruct`
- **Total Parameters**: `494,032,384` (~494M)
- **Constraint Check**: Strictly under 1B parameters
- **Fine-Tuning Method**: PEFT / LoRA
- **LoRA Configuration**: Rank = 16, Alpha = 32, applied to projection layers
- **Compute Budget**: 1× NVIDIA T4 GPU
- **Estimated Runtime**: ~35–45 minutes end-to-end

#### Tasks Solved
- **Task A (Topic Classification)**: Predict one of 7 categories:
  - `business`
  - `entertainment`
  - `health`
  - `politics`
  - `religion`
  - `sports`
  - `technology`

- **Task B (Headline Generation)**: Generate a short headline in the same language as the source text

---

### 🚀 How to Run on Kaggle
1. Open Kaggle and create a new notebook.
2. Set the accelerator to **GPU T4 x1**.
3. Ensure **Internet** is enabled so the model can be downloaded from Hugging Face.
4. Upload the notebook file.
5. Attach the competition dataset in the notebook input folder.
6. Run all cells from top to bottom.
7. Download the generated `submission.csv` and submit it to the competition.

The notebook is built to automatically find the required CSV files in common Kaggle/local paths, so it is designed to be easy to reproduce without manual path changes.

---

### 🧠 Model Training and Evaluation Pipeline
The project follows a structured, reproducible workflow:

1. Load and inspect the training/test CSV files
2. Create a stratified validation split
3. Initialize the tokenizer and model
4. Build language-aware prompts for classification and generation
5. Run a zero-shot baseline
6. Fine-tune the model with LoRA
7. Evaluate baseline vs tuned model on the dev set
8. Generate predictions on the full test set
9. Validate output structure and export the final submission

---

### 🎯 Built-In Evaluation & Checks
This notebook includes several validation features to support competition-grade reproducibility:

- **Automatic parameter-size verification**
  - Confirms that the model is under the 1B parameter limit
- **Zero-shot baseline reporting**
  - Compares base model performance before fine-tuning
- **Side-by-side benchmark table**
  - Baseline vs LoRA fine-tuned model
  - Includes macro-F1, generation score, and final merged score
- **Per-language breakdown**
  - Performance tracked for Hausa, Yoruba, Igbo, and Pidgin
- **Submission integrity validation**
  - Correct row count
  - Correct column names
  - No nulls or blank predictions
  - Only valid topic labels

---

### ✅ Expected Output
The final pipeline exports a valid submission dataset in the required long format:
- `<id>_topic`
- `<id>_headline`

This produces the correct number of rows for the competition, with each article generating two predictions.

---

### 📌 Summary
This project demonstrates a lightweight, practical approach to multilingual Nigerian-language NLP using a compact causal LM with LoRA fine-tuning. It combines classification and generation in a single pipeline, remains compatible with free-tier GPU constraints, and is designed for easy reuse in Kaggle or Colab environments.
