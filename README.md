# RAG-Enabled Chatbot tutorial

This repository supports the tutorial **[How to Create Your Own RAG-Enabled Chatbot for Text Simplification Tasks]([https://medium.com/...](https://medium.com/@noah.wijnheijmer/how-to-create-your-own-rag-enabled-chatbot-for-text-simplification-tasks-in-any-language-a4a5bb20a215)**, where we build a **Retrieval-Augmented Generation (RAG)** chatbot that simplifies government texts while maintaining context and accuracy.

## 📌 Overview

Large Language Models (LLMs) are powerful but can sometimes produce incorrect or outdated information. **Retrieval-Augmented Generation (RAG)** solves this by incorporating real-time, external knowledge retrieval. This tutorial **requires no coding** and enables **local deployment** using:

- 🛠 **[AnythingLLM](https://anythingllm.com/)** - A local RAG-based AI framework for managing vector databases and knowledge retrieval.
- 💻 **[LM Studio](https://lmstudio.ai/)** - A tool to run and fine-tune LLMs locally without requiring cloud access.

## 🚀 Features

✅ **No coding required** – Set up a local AI chatbot using UI-based tools.  
✅ **Runs locally** – No cloud dependencies; all data stays on your device.  
✅ **Supports multiple languages** – Optimized for Dutch, but works with any language.  
✅ **Custom embedding models** – Uses **text-embedding-bge-m3** for multilingual tasks.  
✅ **Handles structured output** – Returns JSON-formatted responses for clarity.  

## 🏗️ Installation

### 1️⃣ Install LM Studio
1. Download and install [LM Studio](https://lmstudio.ai/) for your OS.
2. Enable **Power User Mode** under **Settings**.
3. Load your chosen LLM model from Hugging Face (e.g., `GEITje-7B-ultra`).

### 2️⃣ Install AnythingLLM
1. Download [AnythingLLM](https://anythingllm.com/).
2. Install it **locally** or via **Docker** (recommended for multi-user environments).
3. Connect it to your **vector database** (e.g., LanceDB).

### 3️⃣ Prepare Data for RAG
- Collect **text datasets** from government sources (PDFs, DOCX, CSVs, etc.).
- Use **web scraping** if needed to fetch the latest policy data.
- Store cleaned data in the **vector database**.

### 4️⃣ Configure RAG Pipeline
- Create **text embeddings** using LM Studio.
- Set up **vector retrieval** in AnythingLLM.
- **Optimize prompts** in LM Studio under **Inference Settings**.

## 🔬 Training Details

[A fine-tuned version](https://huggingface.co/Nelis5174473/GovLLM-7B-ultra) of the [GEITje-7B-ultra](https://huggingface.co/BramVanroy/GEITje-7B-ultra) was loaded to compare to the RAG enabled results using the following **training hyperparameters**:

### **Training Hyperparameters**
- **block_size**: `1024`
- **model_max_length**: `2048`
- **padding**: `right`
- **mixed_precision**: `fp16`
- **learning_rate (lr)**: `0.00003`
- **epochs**: `3`
- **batch_size**: `2`
- **optimizer**: `adamw_torch`
- **scheduler**: `linear`
- **quantization**: `int8`
- **peft**: `true`
- **lora_r**: `16`
- **lora_alpha**: `16`
- **lora_dropout**: `0.05`

### **Training Results**
| Epoch  | Loss  | Grad_norm | Learning Rate | Step |
|--------|------|----------|---------------|------|
| 0.14   | 1.3183 | 0.6038 | 1.3888e-05 | 25/540 |
| 0.42   | 1.0220 | 0.4180 | 2.8765e-05 | 75/540 |
| 0.69   | 0.9251 | 0.4119 | 2.5679e-05 | 125/540 |
| 0.97   | 0.9260 | 0.4682 | 2.2592e-05 | 175/540 |
| 1.25   | 0.8586 | 0.5338 | 1.9506e-05 | 225/540 |
| 1.53   | 0.8767 | 0.6359 | 1.6420e-05 | 275/540 |
| 1.80   | 0.8721 | 0.6137 | 1.3333e-05 | 325/540 |
| 2.08   | 0.8469 | 0.7310 | 1.0247e-05 | 375/540 |
| 2.36   | 0.8324 | 0.7945 | 7.1605e-05 | 425/540 |
| 2.64   | 0.8170 | 0.8522 | 4.0741e-05 | 475/540 |
| 2.91   | 0.8185 | 0.8562 | 9.8765e-05 | 525/540 |
