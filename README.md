# 🏥 Medical Chatbot - AI-Powered Healthcare Assistant

An intelligent medical chatbot that provides accurate health information by retrieving relevant content from medical literature using RAG (Retrieval-Augmented Generation) technology.

![Python](https://img.shields.io/badge/Python-3.10-blue)
![LangChain](https://img.shields.io/badge/LangChain-Latest-green)
![Pinecone](https://img.shields.io/badge/Pinecone-Vector_DB-orange)
![Gemini](https://img.shields.io/badge/Google-Gemini_AI-red)

## 🌟 Features

- **Semantic Search**: Find relevant medical information using vector embeddings
- **Context-Aware Responses**: Answers based on actual medical documents
- **Source Attribution**: Cites source documents for transparency
- **Safe & Responsible**: Includes disclaimers and directs users to healthcare professionals
- **Easy to Use**: Simple query interface for health-related questions

## 🏗️ Architecture

```
User Query → Embedding Model → Pinecone Vector Search → 
Retrieved Documents → Gemini LLM → Contextualized Answer
```

**Tech Stack:**
- **LangChain**: Orchestration framework
- **HuggingFace Embeddings**: Text-to-vector conversion (all-MiniLM-L6-v2)
- **Pinecone**: Vector database for semantic search
- **Google Gemini**: Large language model for answer generation
- **PyPDF**: Document loading and processing

## 📋 Prerequisites

- Python 3.10+
- Pinecone account and API key
- Google Gemini API key
- Conda or pip for package management

## 🚀 Installation

### 1. Clone the repository
```bash
git clone https://github.com/zainop23/medical-chatbot.git
cd medical-chatbot
```

### 2. Create virtual environment
```bash
conda create -n medibot python=3.10 -y
conda activate medibot
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Set up environment variables
Create a `.env` file in the project root:
```env
PINECONE_API_KEY=your_pinecone_api_key_here
GOOGLE_API_KEY=your_google_gemini_api_key_here
```

### 5. Add medical documents
Place your PDF medical documents in the `data/` folder.

## 📦 Requirements

```txt
langchain==0.3.26
langchain-community
langchain-google-genai
langchain-pinecone
pinecone-client
sentence-transformers
pypdf
python-dotenv
numpy<2
torch
flask
```

## 💻 Usage

### Run the Jupyter Notebook
```bash
jupyter notebook research/trials.ipynb
```

### Run the Flask Application
```bash
python app.py
```

Then open your browser to `http://localhost:8080`

### Basic Usage Example
```python
# Ask a question
response = rag_chain.invoke({"input": "What is acne and how is it treated?"})
print(response['answer'])
```

## 📊 Project Structure

```
medical-chatbot/
│
├── data/                       # Medical PDF documents
├── research/
│   └── trials.ipynb           # Development notebook
├── src/
│   ├── helper.py              # Helper functions
│   └── prompt.py              # Prompt templates
├── static/
│   └── style.css              # CSS styling
├── templates/
│   └── chat.html              # Chat interface
├── .env                       # Environment variables (not in repo)
├── .gitignore
├── README.md
├── requirements.txt
├── setup.py                   # Package setup
└── app.py                     # Flask application
```

## 🔧 Configuration

### Embedding Model
Current: `sentence-transformers/all-MiniLM-L6-v2` (384 dimensions)

To change:
```python
embeddings = HuggingFaceEmbeddings(
    model_name="your-preferred-model"
)
```

### Text Chunking
```python
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=500,      # Adjust based on your needs
    chunk_overlap=20     # Overlap to maintain context
)
```

### Retrieval Settings
```python
retriever = docsearch.as_retriever(
    search_type="similarity",
    search_kwargs={"k": 3}  # Number of documents to retrieve
)
```

## 🎯 How It Works

1. **Document Processing**
   - PDFs are loaded from the `data/` folder
   - Text is extracted and split into chunks
   - Chunks are converted to embeddings

2. **Vector Storage**
   - Embeddings are stored in Pinecone
   - Metadata (source files) is preserved

3. **Query Processing**
   - User question is converted to embedding
   - Similar document chunks are retrieved
   - Gemini generates answer using retrieved context

4. **Response Generation**
   - LLM reads context and question
   - Generates accurate, contextual answer
   - Returns answer with source attribution

## ⚠️ Limitations & Disclaimers

- **Not a Medical Professional**: This chatbot provides information only, not medical advice
- **Always Consult Doctors**: Users should consult healthcare professionals for diagnosis and treatment
- **Context-Dependent**: Answers are limited to the documents in the database
- **Not for Emergencies**: Direct users to emergency services for urgent medical situations

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- Built with [LangChain](https://langchain.com/)
- Powered by [Google Gemini](https://ai.google.dev/)
- Vector storage by [Pinecone](https://www.pinecone.io/)
- Embeddings from [HuggingFace](https://huggingface.co/)

## 📧 Contact

Zain - [@zainop23](https://github.com/zainop23)

Project Link: [https://github.com/zainop23/medical-chatbot](https://github.com/zainop23/medical-chatbot)

## 🔮 Future Enhancements

- [ ] Web interface improvements
- [ ] Multi-language support
- [ ] Voice input/output
- [ ] Conversation history
- [ ] Fine-tuned medical model
- [ ] Integration with medical APIs
- [ ] Mobile application

---

**⭐ If you find this project helpful, please give it a star!**
