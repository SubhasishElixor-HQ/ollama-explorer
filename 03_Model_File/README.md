# Ollama Modelfile — Custom AI Model

A practical guide to creating and running custom AI models using **Ollama Modelfile**.

This project demonstrates how to customize an existing Ollama model with a custom system prompt and model parameters, then create a new model named `omnify:latest`.

---

## 📌 Project Overview

A **Modelfile** is a configuration file used by Ollama to create a customized model.

It allows you to define:

* Base model
* System prompt
* Model behavior
* Temperature
* Context size
* Other runtime parameters
* Optional templates and adapters

### Basic Flow

```text
Existing Ollama Model
        │
        ▼
   Modelfile
        │
        ├── Base Model
        ├── System Prompt
        ├── Parameters
        └── Configuration
        │
        ▼
 Custom Ollama Model
        │
        ▼
   omnify:latest
        │
        ▼
   ollama run
```

---

# 🧠 What is Ollama?

[Ollama](https://ollama.com/) is a platform for running Large Language Models (LLMs) locally.

It allows developers to:

* Run LLMs locally
* Download open models
* Create custom models
* Customize model behavior
* Build AI applications
* Use models through an API
* Integrate LLMs with Python and other applications

---

# 📁 Project Structure

```text
03_Model_File/
│
├── Modelfile
│
└── README.md
```

> **Important:** The filename must be exactly `Modelfile`.
>
> Do not use `Modelfile.txt`.

---

# ⚙️ Modelfile

Example:

```text
FROM qwen3:4b

SYSTEM """
You are Omnify, an AI assistant.
You help users solve problems clearly and accurately.
Give practical, useful, and concise answers.
"""

PARAMETER temperature 0.7
PARAMETER num_ctx 4096
```

---

# 🔍 Modelfile Explanation

## 1. FROM

```text
FROM qwen3:4b
```

`FROM` specifies the base model.

For example:

```text
FROM qwen3:4b
```

or:

```text
FROM gemma3:latest
```

or:

```text
FROM llama3.2:latest
```

The base model must already be available in Ollama.

Check installed models:

```bash
ollama list
```

---

# 2. SYSTEM

```text
SYSTEM """
You are Omnify, an AI assistant.
You help users solve problems clearly and accurately.
Give practical, useful, and concise answers.
"""
```

The `SYSTEM` instruction defines the behavior and personality of the model.

For example, you can create a coding assistant:

```text
SYSTEM """
You are a professional programming assistant.
Help users write clean, correct, and understandable code.
Explain errors and provide practical solutions.
"""
```

---

# 3. PARAMETER

Parameters control how the model generates responses.

### Temperature

```text
PARAMETER temperature 0.7
```

Temperature controls response randomness.

General idea:

```text
0.0 → More deterministic
0.3 → Focused
0.7 → Balanced
1.0 → More creative
```

---

### Context Size

```text
PARAMETER num_ctx 4096
```

This controls the context window used by the model.

A larger context can allow the model to work with more input, but it can also increase memory usage.

---

# 🚀 Installation

Install Ollama from the official website:

[Ollama](https://ollama.com/?utm_source=chatgpt.com)

Verify installation:

```bash
ollama --version
```

---

# 📥 Download a Base Model

For example:

```bash
ollama pull qwen3:4b
```

Check installed models:

```bash
ollama list
```

Example:

```text
NAME              SIZE
qwen3:4b          ...
gemma3:latest     ...
llama3.2:latest   ...
```

---

# 🛠️ Create the Custom Model

Open your project directory:

```cmd
cd C:\Users\subha\OneDrive\Desktop\Ollama\03_Model_File
```

Make sure the directory contains:

```text
Modelfile
README.md
```

Then create the model:

```cmd
ollama create omnify:latest -f Modelfile
```

If successful, Ollama will create:

```text
omnify:latest
```

---

# ▶️ Run the Model

```bash
ollama run omnify:latest
```

Now you can communicate with your custom model directly from the terminal.

Example:

```text
>>> Hello Omnify

Hello! How can I help you today?
```

---

# 📋 Manage the Model

### List models

```bash
ollama list
```

### Show model information

```bash
ollama show omnify:latest
```

### Run model

```bash
ollama run omnify:latest
```

### Remove model

```bash
ollama rm omnify:latest
```

---

# 🔄 Modify the Model

If you change the `Modelfile`, recreate the model:

```bash
ollama create omnify:latest -f Modelfile
```

Then run:

```bash
ollama run omnify:latest
```

---

# 🧪 Testing

After starting the model:

```bash
ollama run omnify:latest
```

Try:

```text
Explain artificial intelligence.
```

```text
Write a Python program to calculate factorial.
```

```text
Explain machine learning in simple terms.
```

```text
Create a roadmap for learning AI engineering.
```

---

# 🧩 Useful Modelfile Instructions

A Modelfile can contain several configuration instructions.

Common instructions include:

```text
FROM
SYSTEM
PARAMETER
TEMPLATE
ADAPTER
MESSAGE
LICENSE
```

For most beginner projects, the following are enough:

```text
FROM
SYSTEM
PARAMETER
```

---

# 🔐 Local AI

One major advantage of Ollama is that models can run locally on your computer.

```text
User
  │
  ▼
Ollama
  │
  ▼
Local LLM
  │
  ▼
Response
```

This can be useful for development, experimentation, and applications where sending prompts to an external API is undesirable.

---

# 🧑‍💻 Using Ollama with Python

Install the Ollama Python package:

```bash
pip install ollama
```

Example:

```python
import ollama

response = ollama.chat(
    model="omnify:latest",
    messages=[
        {
            "role": "user",
            "content": "Explain machine learning."
        }
    ]
)

print(response["message"]["content"])
```

---

# 🌐 Ollama API

Ollama provides a local API that applications can use to communicate with models.

Typical local endpoint:

```text
http://localhost:11434
```

This makes it possible to build applications using:

* Python
* FastAPI
* JavaScript
* React
* Next.js
* LangChain
* LangGraph

---

# 🏗️ Example AI Application Architecture

```text
                    User
                     │
                     ▼
                Web Application
                     │
                     ▼
                 FastAPI
                     │
                     ▼
                 Ollama API
                     │
                     ▼
              omnify:latest
                     │
                     ▼
                Local LLM
                     │
                     ▼
                  Response
```

---

# 🎯 Learning Objectives

Through this project, you will learn:

* What Ollama is
* What a Modelfile is
* How to customize an LLM
* How to define system instructions
* How to configure model parameters
* How to create custom Ollama models
* How to run local LLMs
* How to integrate Ollama with Python
* How to build applications around local LLMs

---

# 🛠️ Technologies

| Technology | Purpose                      |
| ---------- | ---------------------------- |
| Ollama     | Local LLM runtime            |
| Qwen3      | Base language model          |
| Modelfile  | Model customization          |
| Python     | Application development      |
| FastAPI    | API development              |
| LangChain  | LLM application framework    |
| LangGraph  | Agent/workflow orchestration |

---

# 📚 Commands Cheat Sheet

```bash
# Check Ollama
ollama --version

# List models
ollama list

# Download model
ollama pull qwen3:4b

# Create custom model
ollama create omnify:latest -f Modelfile

# Run custom model
ollama run omnify:latest

# Show model information
ollama show omnify:latest

# Remove model
ollama rm omnify:latest
```

---

# ⚠️ Common Error

### Error

```text
Error: no Modelfile or safetensors files found
```

### Cause

The file may be named:

```text
Modelfile.txt
```

instead of:

```text
Modelfile
```

### Fix on Windows CMD

```cmd
ren Modelfile.txt Modelfile
```

Then:

```cmd
ollama create omnify:latest -f Modelfile
```

---

# 📌 Important Notes

1. `Modelfile` must have no `.txt` extension.
2. The model specified in `FROM` should be available locally or be a valid Ollama model.
3. After modifying `Modelfile`, recreate the custom model.
4. Use `ollama list` to verify installed models.
5. Use `ollama show` to inspect a custom model.

---

# 🚀 Future Improvements

This project can be extended into a complete local AI platform with:

* RAG
* Vector databases
* Document Q&A
* AI agents
* Tool calling
* Web search
* FastAPI backend
* React/Next.js frontend
* LangChain integration
* LangGraph workflows
* Local embeddings
* PostgreSQL + pgvector
* Multi-model routing
* Voice interaction

---

# 👨‍💻 Author

**Subhasish Sahoo**

Computer Science & Artificial Intelligence & Machine Learning

Focused on:

* Artificial Intelligence
* Machine Learning
* Generative AI
* LLMs
* RAG
* AI Agents
* Full-Stack AI Applications

---

## ⭐ Project Goal

The goal of this project is to understand how local Large Language Models can be customized with **Ollama Modelfiles** and integrated into real-world AI applications.

> **Learn → Customize → Run → Integrate → Build**

---
