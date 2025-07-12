# 📘 HyDE-RAG: Hypothetical Document Enhanced PDF QA with LangChain + Groq

This project implements a HyDE-style RAG (Retrieval-Augmented Generation) pipeline to answer questions based on the content of a PDF document.

It uses:

- 🧠 LangChain for chaining prompts and language models

- ⚡ Groq for ultra-fast LLM inference (e.g. Qwen3-32B)

- 📄 FAISS + Sentence Transformers for semantic vector search

- 📚 PyPDFLoader for extracting content from PDFs

# 🚀 Features


- ✅ Automatically chunk and embed PDF content

- ✅ Use a language model to generate a hypothetical document (HyDE) to improve retrieval quality

- ✅ Retrieve top relevant text chunks using vector similarity

- ✅ Use the retrieved chunks as context to generate an accurate final answer

- ✅ Fully offline document search + online LLM reasoning


# 📂 Project Structure

```bash
.
├── hyde_rag.py            # Main script
├── Understanding_Climate_Change.pdf  # Sample PDF
```

# 🛠️ Installation

1. Clone the repository
```bash
git clone https://github.com/tinyzqh/hyde-rag.git
cd hyde-rag
```

2. Create a virtual environment
```bash
conda create -n hyde-rag python=3.11
conda activate hyde-rag
```

3. Install dependencies
```bash
pip install -r requirements.txt
```

# 🔑 Set your Groq API key

Replace the placeholder in the script with your `Groq API key`:
```bash
self.llm_model = ChatGroq(
    model_name="qwen/qwen3-32b",
    groq_api_key="your_groq_api_key"
)
```

# 📄 How It Works

1. **PDF Loading**: The document is loaded and split into overlapping chunks (default: 1000 tokens, 200 overlap).

2. **Vector Embedding**: Each chunk is embedded using all-MiniLM-L6-v2 from SentenceTransformers and stored in a FAISS vector index.

3. **HyDE Prompting**: A language model is prompted to generate a "hypothetical" detailed answer based on the user's question.

4. **Vector Search**: The generated hypothetical document is used to retrieve the most semantically similar chunks from the vector store.

5. **Final Answering**: The top retrieved chunks are provided as context to the LLM to generate the final, grounded answer.
