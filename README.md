# 🧠 RAG Evaluation using RAGAs Framework 

The purpose of this evaluation is to assess how well the system retrieves relevant context and generates faithful, relevant answers for a given user query. The solution avoids reliance on paid APIs (like OpenAI or Anthropic) and instead leverages efficient, **free and local models**. No paid APIs required.

---

## 📌 Objective

The main objective of this assignment is to evaluate a list of generated RAG outputs using well-defined metrics that assess:

- 🔎 **Faithfulness**: Is the answer grounded in the retrieved context?
- 🧩 **Answer Relevancy**: Does the answer address the user’s question appropriately?
- 🧠 **Context Precision**: Is the provided context actually relevant to the query?

---

## 🧭 Approach

### ✅ Step 1: Load Logs
We begin by reading the `logs.json` file which contains structured data:
- System-generated prompts (`context`)
- User queries (`user_input`)
- Model-generated responses (`answer`)

### ✅ Step 2: Preprocessing
From each entry in the logs, we extract:
- The context provided to the model
- The user’s query
- The assistant’s response

These are structured into three lists: `contexts`, `queries`, and `answers`.

### ✅ Step 3: Embedding with SentenceTransformer
We load the [BAAI/bge-large-en-v1.5](https://huggingface.co/BAAI/bge-large-en-v1.5) model using the `sentence-transformers` library to convert:
- Contexts
- Queries
- Answers  
...into dense vector representations (embeddings).

### ✅ Step 4: Similarity-Based Scoring
We use cosine similarity to calculate:
- `faithfulness`: similarity between context and answer
- `answer_relevancy`: similarity between query and answer

This gives us a semantic-level understanding of how well the answer is grounded and how relevant it is.

### ✅ Step 5: Output Results
We save the results into a `ragas_output.json` file which contains:

[
  {
    "id": "sample_id_1",
    "faithfulness": 0.87,
    "answer_relevancy": 0.91
  }
  ... more samples
]

---

## 🧰 Libraries Used

| Library                 | Purpose                               |
| ----------------------- | ------------------------------------- |
| `sentence-transformers` | For generating embeddings             |
| `torch`                 | Backend used by embedding models      |
| `transformers`          | HuggingFace model support             |
| `json`                  | Reading and writing input/output data |
| `pandas`                | (Optional) Data inspection            |

---

## ⚙️ Assumptions & Simplifications

* 🧪 **No external API usage**: We deliberately avoided using paid APIs like OpenAI or Anthropic to make the evaluation **cost-free and locally runnable**.
* 📉 **Only two RAGAS metrics** are evaluated: `faithfulness` and `answer_relevancy`. `context_precision` was skipped as the context wasn't retrieved in multiple chunks, making this metric                                                 inapplicable to the simplified, single-context format used in the evaluation.
* ⏱️ **Timeouts/NaNs**: In earlier local LLM versions, some timeouts were observed, but with this simplified embedding approach, it's avoided completely.
* 🧼 **Data cleaning is minimal**: Assumes `logs.json` is well-structured and consistent.

---

## 🚀 How to Use

> ⚡ This implementation is fully runnable inside **Google Colab**.

### Steps:

1. Open the [Google Colab Notebook](https://colab.research.google.com/) 📎  
2. Upload the `logs.json` file in Google Colab  
3. Run the notebook from top to bottom  
4. Get the evaluation results saved as `ragas_output.json`

---

## 📁 Repository Contents

| File                     | Description                            |
| ------------------------ | -------------------------------------- |
| `RAGAs_Assignment.ipynb` | Main Colab notebook with full pipeline |
| `logs.json`              | Input conversation data                |
| `ragas_output.json`      | Final output scores per item           |
| `README.md`              | This documentation file                |

---

## 🔗 Google Colab Link

👉 **Run this notebook here**: [🔗 Open in Colab](https://colab.research.google.com/drive/1slgi2FDBVhSiPtLKM5st8bf4C-zrt_qA?usp=drive_link)

---

## 🙌 Final Thoughts

The project showcases a simple but effective way to evaluate RAG outputs without relying on cloud APIs. It demonstrates the ability to use open-source tools to generate meaningful insights from model outputs in a structured, explainable way.

If needed, this notebook can be further extended to:

* Include `context_precision`
* Visualize results in tabular format
* Evaluate larger datasets

---

## 📬 Contact

If you have questions, feedback, or ideas, feel free to connect.

Happy coding! 🎉
