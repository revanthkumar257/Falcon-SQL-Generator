
# 🧠 Falcon SQL Generator

A lightweight, fine-tuned Falcon-1B model that translates **natural language questions** into **SQL queries** using a **LoRA-adapted architecture**. This project combines **prompt engineering**, **few-shot learning**, and **Retrieval-Augmented Generation (RAG)** via FAISS to generate accurate SQL from user prompts.


## 🚀 Project Highlights

* 🔧 **Model**: [Falcon-1B](https://huggingface.co/tiiuae/falcon-rw-1b) + [LoRA](https://arxiv.org/abs/2106.09685) (PEFT)
* 🧠 **RAG**: Contextual SQL generation using schema-aware prompts from FAISS-based semantic retrieval
* 📄 **Dataset**: Synthetic Spider-style (text-to-SQL) examples
* 🎯 **Goal**: Enable users to ask natural language questions and receive structured SQL queries
* 🌐 **UI**: Built with **Gradio** and **Streamlit** for live demo and user interaction


## 🔍 How It Works

### 🧩 1. Data Preparation

* Created synthetic question-SQL pairs using Spider-style dataset format
* Schema-aware design enables adaptability to different table structures

### ⚙️ 2. Model Fine-Tuning

* Used Hugging Face `transformers` + `peft` for efficient **LoRA fine-tuning**
* Model: `tiiuae/falcon-rw-1b`
* Trained on curated prompts:

  ```text
  ### Schema Info:
  employees(id, name, department, salary)

  ### Question:
  List all employees in Sales.

  ### SQL:
  SELECT * FROM employees WHERE department = 'Sales';
  ```

### 🧠 3. RAG with FAISS

* Retrieved top-k relevant schema chunks using `SentenceTransformerEmbeddings` and `FAISS`
* Combined with user query to dynamically construct final prompt

### 🎯 4. Inference & Generation

* Tokenized prompt passed to fine-tuned Falcon
* Generated SQL parsed and presented via Gradio or Streamlit app


## 🌐 Run the Gradio App

```bash
pip install gradio transformers peft sentence-transformers faiss-cpu
python gradio_app.py
```


## 🖥️ Run the Streamlit App

```bash
pip install streamlit transformers peft
streamlit run app.py
```

---

## 🧪 Example

**Input**:

> *"List employees earning more than 50000"*

**Generated SQL**:

```sql
SELECT * FROM employees WHERE salary > 50000;
```

## 📦 Tech Stack

* 🧠 Falcon-1B (via Hugging Face)
* 🔁 LoRA + PEFT for parameter-efficient fine-tuning
* 💬 LangChain for prompt management
* 📚 FAISS + Sentence Transformers for semantic search
* 🌐 Gradio & Streamlit for app interface

---

## 🔗 Links

* 🤖 Model: [Falcon RW 1B on Hugging Face](https://huggingface.co/tiiuae/falcon-rw-1b)
* 🔧 LoRA Adapter: [revanthkumarg/falcon-sql-lora](https://huggingface.co/revanthkumarg/falcon-sql-lora)
* 💻 GitHub Repo: [https://github.com/revanthkumar257/falcon-sql-project](https://github.com/revanthkumar257/falcon-sql-project) 


## 🙌 Acknowledgements

* [Hugging Face Transformers](https://huggingface.co/transformers)
* [LangChain](https://www.langchain.com/)
* [FAISS by Facebook AI](https://github.com/facebookresearch/faiss)
* [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685)


