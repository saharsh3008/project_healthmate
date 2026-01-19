# HealthMate: AI-Powered Medical Chatbot 🩺🤖

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python)
![Flask](https://img.shields.io/badge/Flask-Web%20Framework-lightgrey?style=for-the-badge&logo=flask)
![LangChain](https://img.shields.io/badge/LangChain-RAG%20Framework-orange?style=for-the-badge&logo=chainlink)
![Pinecone](https://img.shields.io/badge/Pinecone-Vector%20Database-green?style=for-the-badge&logo=database)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT%20Models-black?style=for-the-badge&logo=openai)
![License](https://img.shields.io/badge/License-MIT-purple?style=for-the-badge)

## 📌 Overview

**HealthMate** is an intelligent, domain-specific medical chatbot designed to provide concise and accurate health information. Built on a robust **Retrieval-Augmented Generation (RAG)** architecture, HealthMate ingests medical knowledge from PDF documents, indexes them into a vector database, and uses Large Language Models (LLMs) to answer user queries with improved context and reduced hallucinations.

Whether you're looking for quick symptom checks or detailed medical explanations, HealthMate serves as a reliable conversational assistant, leveraging the power of **LangChain**, **Pinecone**, and **OpenAI**.

---

## 🚀 Key Features

*   **📚 Custom Knowledge Base**: Ingests and comprehends medical data directly from PDF documents (e.g., medical books, research papers).
*   **🧠 Semantic Search**: Uses high-performance embeddings (`sentence-transformers/all-MiniLM-L6-v2`) to find the most relevant information for any query.
*   **⚡ Fast & Scalable Retrieval**: Powered by **Pinecone's** serverless vector database for millisecond-latency searches.
*   **💬 Natural Language Answers**: Generates human-like, context-aware responses using **OpenAI's GPT models**.
*   **💻 Interactive Web Interface**: A clean, responsive chat interface built with **Flask** and **HTML/CSS**.
*   **📄 Source Traceability**: The RAG pipeline ensures answers are grounded in the provided medical documents.

---

## 🏗️ Architecture & How It Works

HealthMate follows a modern RAG pipeline architecture:

1.  **Data Ingestion 📥**:
    *   Medical PDFs are loaded from the `Data/` directory.
    *   Content is extracted and split into smaller, manageable text chunks (500 characters) using `RecursiveCharacterTextSplitter`.

2.  **Vectorization & Indexing 📐**:
    *   Each text chunk is converted into a 384-dimensional vector using the **Hugging Face** embedding model (`sentence-transformers/all-MiniLM-L6-v2`).
    *   These vectors are upserted into a **Pinecone** vector index (`medicalbot`).

3.  **Retrieval (Question Asking) 🔍**:
    *   When a user asks a question, the system converts the query into a vector.
    *   Pinecone performs a similarity search to find the top 3 most relevant text chunks from the knowledge base.

4.  **Generation (Answering) 💡**:
    *   The retrieved text chunks + the user's question are combined into a prompt.
    *   This prompt is sent to the **OpenAI LLM**.
    *   The LLM generates a concise answer based *strictly* on the retrieved context.

---

## 🛠️ Tech Stack

*   **Backend**: Python, Flask
*   **Orchestration**: LangChain
*   **Vector Database**: Pinecone
*   **Embeddings**: Hugging Face (`sentence-transformers`)
*   **LLM**: OpenAI (GPT-3.5/4)
*   **Frontend**: HTML, CSS, JavaScript (Vanilla)
*   **Containerization**: Docker (Optional)

---

## 📂 Project Structure

```bash
project_medical-chatbot/
├── Data/                   # Directory to store medical PDFs
├── src/
│   ├── helper.py           # Functions for data loading, splitting, and embedding
│   ├── prompt.py           # System prompts for the LLM
│   └── __init__.py
├── templates/              # HTML templates for Flask
│   └── chat.html
├── static/                 # Static assets (CSS/JS)
├── app.py                  # Main Flask application file
├── store_index.py          # Script to ingest data and update Pinecone index
├── setup.py                # Package setup script
├── requirements.txt        # Python dependencies
├── .env                    # Environment variables (API Keys)
└── README.md               # Project documentation
```

---

## 🏁 Getting Started

Follow these steps to set up HealthMate locally.

### 1. Prerequisites
*   Python 3.9 or higher
*   Git
*   API Keys for:
    *   [Pinecone](https://www.pinecone.io/)
    *   [OpenAI](https://openai.com/)

### 2. Clone the Repository
```bash
git clone https://github.com/yourusername/HealthMate.git
cd HealthMate
```

### 3. Create a Virtual Environment (Recommended)
```bash
conda create -n healthmate python=3.10
conda activate healthmate
```

### 4. Install Dependencies
```bash
pip install -r requirements.txt
```

### 5. Configure Environment Variables
Create a `.env` file in the root directory and add your API keys:
```bash
PINECONE_API_KEY=your_pinecone_api_key
OPENAI_API_KEY=your_openai_api_key
```

### 6. Build the Vector Index
Place your medical PDF files in the `Data/` folder. Then run the indexing script to structure and upload data to Pinecone.
```bash
python store_index.py
```
*Note: This may take a few minutes depending on the size of your documents.*

### 7. Run the Application
Start the Flask web server:
```bash
python app.py
```
The application will be running at `http://localhost:8080`.

---

## 📸 Screenshots

*(Add screenshots of the chat interface here to show users what it looks like)*

---

## 🤝 Contributing

Contributions are welcome! Please fork the repository and create a pull request with your features or fixes.

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.
