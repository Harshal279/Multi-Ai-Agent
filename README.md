# Multi-Agent AI System
### Project Needs 5min to load as it is deployed on render free tier

Live Project link : https://multi-ai-agent-final.onrender.com/
## Overview

The **Multi-Agent AI System** is an intelligent, modular framework designed to process diverse user queries by delegating them to specialized AI agents.  
Built with **Python** and **Flask**, it integrates **Large Language Models (LLMs)** via the **Groq API**, combined with **Retrieval-Augmented Generation (RAG)** for precise, context-aware responses.

This project is ideal for **research assistance**, **document-based Q&A**, and **real-time knowledge retrieval** applications.

---

## Key Features

### Intelligent Query Routing
A **Controller Agent** analyzes incoming queries and dynamically decides which specialized agent(s) to invoke.

### Specialized Agents

1. **PDF RAG Agent**  
   - Processes and queries uploaded PDF documents.  
   - Uses **FAISS** for vector search and **SentenceTransformers** for embeddings.

2. **Web Search Agent**  
   - Performs real-time searches using **DuckDuckGo**, with **SerpAPI** as an optional fallback.  
   - Synthesizes relevant results for user queries.

3. **ArXiv Agent**  
   - Searches academic papers on **ArXiv**.  
   - Returns research summaries and relevant abstracts.

### Web Interface
A simple **Flask-based UI** for:
- Submitting text queries  
- Uploading and querying PDFs  
- Viewing logs and system activity

### Logging & Monitoring
- Comprehensive **JSON-based logs** for every system event, agent decision, and API response.  
- Error handling with meaningful fallback messages.

### Privacy-Focused
- Uploaded PDFs are **immediately deleted after ingestion**.  
- Only text chunks and embeddings are retained locally in `rag_data/`.

---

## System Architecture

![Architecture Diagram](https://github.com/user-attachments/assets/4ec6d2db-731b-42f5-9940-677eee6c6b63)

---

## Key Technologies

| Component | Technology |
|------------|-------------|
| **Backend** | Flask |
| **LLM Inference** | Groq API |
| **Vector Search** | FAISS |
| **Embeddings** | SentenceTransformers |
| **PDF Processing** | pdfplumber, PyMuPDF |
| **Web Search** | duckduckgo-search, SerpAPI |
| **Logging** | Custom JSON logging |
| **Deployment** | Gunicorn (production-ready) |

---

## Setup Instructions

### **1. Prerequisites**
- Python **3.8+**
- Git
- Groq API key (Free tier available at [console.groq.com](https://console.groq.com))
- Optional: SerpAPI key (for Google Search fallback)

---

### **2. Clone the Repository**
```bash
git clone <https://github.com/Harshal279/Multi-Ai-Agent>
cd <Multi-Ai-Agent>
```

### **3. Install Dependencies**
```bash
pip install -r requirements.txt
```
### **4. Set Environment Variables**
Create a .env file in the project root:
```bash
GROQ_API_KEY=your_groq_api_key_here
SERPAPI_KEY=your_serpapi_key_here      # Optional
SECRET_KEY=your_flask_secret_key_here  # Optional, defaults to dev key
```

Environment variables are automatically loaded using python-dotenv.

### **5. Initialize the System**
On the first run, sample PDFs (e.g., AI ethics dialogs) are automatically generated and indexed by the PDF RAG Agent.
Run the application:
python app.py
The FAISS index will be created in rag_data/.

### **6. Access the Web Interface**
Open: http://localhost:7860
For production deployment:
gunicorn app:app
Or specify a custom port:
```bash
export PORT=8080
gunicorn app:app
```
## Testing the System
Task	Example Query
General Knowledge	“What are recent trends in AI ethics?”
PDF Q&A	Upload a PDF and ask “Summarize this document.”
Research Papers	“Find latest ArXiv papers on computer vision.”

## Logs can be viewed via:
The UI Log Viewer, or
The /logs endpoint in your browser.

## Dependencies
Below are the key packages used in the project:
```bash
Package	Version	Description
Flask	3.0.0	Web framework
groq	0.4.1	LLM API client
faiss-cpu	1.7.4	Vector similarity search
sentence-transformers	2.2.2	Embedding generation
PyMuPDF	1.23.8	PDF handling
duckduckgo-search	3.9.6	Web search
numpy	1.24.3	Numerical computing
torch	2.1.0	ML backend
gunicorn	21.2.0	Production server
```
Install all dependencies via:
```bash
pip install -r requirements.txt
```
## Expected Outputs

Below are sample outputs of the system in action:

<img width="1155" height="725" alt="Screenshot 2025-10-06 175441" src="https://github.com/user-attachments/assets/faf4b786-3917-4c39-9d2c-d4ebe94fef40" />
<img width="1061" height="902" alt="Screenshot 2025-10-06 175838" src="https://github.com/user-attachments/assets/7a9d9c46-1828-4a47-b7f8-c6c7e6ae79f5" />
<img width="1113" height="925" alt="Screenshot 2025-10-06 175728" src="https://github.com/user-attachments/assets/affbec87-fc61-4a9a-8ae8-a2189cbb4a28" />
<img width="1048" height="912" alt="Screenshot 2025-10-06 175646" src="https://github.com/user-attachments/assets/f60f5179-0ce1-4c67-9181-00ba592fa90e" />



## Error Handling:
Graceful fallbacks for unavailable or empty results (e.g., “No results found”).
Resilient exception handling with detailed logging for:
API rate limits
Network timeouts
Missing or invalid inputs
Retention & Privacy Policy
Uploaded PDF files are deleted immediately after processing.
Only text embeddings (without PII) are stored locally for querying.
Data is stored under rag_data/ for persistent context retrieval.
## Future Improvements
Add support for multi-modal inputs (images, CSVs).
Integrate advanced ranking for retrieved results.
Expand specialized agents (e.g., for code generation, summarization, and analytics).
Dockerize the project for easier deployment.

Author
Harshal Ghoradkar




