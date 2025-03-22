
# Document QA Chatbot with LangChain and Streamlit

This repository contains a **Document Question-Answering (QA) Chatbot** built using **LangChain** and **Streamlit**. The chatbot allows users to upload documents (PDF, CSV, TXT), ask questions, and receive answers based on the content of the uploaded documents. It leverages **vector embeddings** and **language models** (OpenAI or Llama3) for semantic search and response generation.

---

## **Features**
- **Document Upload**: Supports multiple file types (PDF, CSV, TXT).
- **Semantic Search**: Uses vector embeddings (OpenAI or Cohere) for retrieving relevant document chunks.
- **Conversational Interface**: Built with Streamlit, providing a user-friendly chat interface.
- **Memory**: Maintains chat history for context-aware responses.
- **Customizable**: Supports different language models (OpenAI GPT-3.5, Llama3) and embedding models (OpenAI, Cohere).

---

## **Technologies Used**
- **LangChain**: For building the document QA pipeline.
- **Streamlit**: For the web-based user interface.
- **Chroma**: Vector database for storing and retrieving document embeddings.
- **OpenAI/Cohere**: For generating embeddings and powering the language model.
- **Ollama**: For running the Llama3 model locally.

---

## **Setup Instructions**

### **1. Prerequisites**
- Python 3.8 or higher.
- An OpenAI API key (if using OpenAI embeddings or GPT-3.5).
- A Cohere API key (if using Cohere embeddings).
- Ollama installed (if using Llama3 locally).

### **2. Clone the Repository**

- ```git clone git@github.com:vaibhavsemwalwork/DocumentRAGTool.git```


### 3. Set Up Environment Variables

- Create a .env file in the root directory.

- Add the following variables:
```
OPENAI_API_KEY=your_openai_api_key
COHERE_API_KEY=your_cohere_api_key
PERSIST_DIRECTORY=./vectorstore
EMBEDDINGS_MODEL_NAME=openai  # or "Cohereembeddings"
MODEL_TYPE=OpenaAI  # or "Llama3"
```

### 4. Install Dependencies
```pip install -r requirements.txt```
### 5.  Run the Application
```streamlit run app.py```

### 6. Access the Chatbot
- Open your browser and navigate to ```http://localhost:8501.```

- Upload documents and start asking questions!

# How It Works
1. **Document Processing**:

Users upload documents (PDF, CSV, TXT) via the Streamlit interface.The documents are split into smaller chunks using a text splitter.Each chunk is converted into a vector embedding using OpenAI or Cohere embeddings.

2. **Vector Database**:
The embeddings are stored in a Chroma vector database.The vector store is persisted in the PERSIST_DIRECTORY for reuse across sessions.

3. **Query Handling**:
When a user asks a question:

- The query is converted into an embedding.

- The vector database performs a semantic search to retrieve the most relevant document chunks.

- The retrieved chunks are passed to the language model (OpenAI GPT-3.5 or Llama3) to generate a response.

4. **Chat Interface**:
The chatbot maintains a conversation history using ConversationBufferMemory.Users can ask follow-up questions and receive context-aware responses.

# Customization
1. **Embedding Models**:

To switch between OpenAI and Cohere embeddings, update the EMBEDDINGS_MODEL_NAME in the .env file:

```
EMBEDDINGS_MODEL_NAME=openai  # or "Cohereembeddings"
```

2. **Language Models**:
To switch between OpenAI GPT-3.5 and Llama3, update the MODEL_TYPE in the .env file:

```
MODEL_TYPE=OpenaAI  # or "Llama3"
```

3. **Chunk Size and Overlap**:

Adjust the chunk_size and chunk_overlap parameters in the code for better document processing:

```
chunk_size = 500
chunk_overlap = 50
```

# Troubleshooting

1. **API Key Errors**:

Ensure that the API keys in the .env file are correct and valid.If using OpenAI, verify that your account has sufficient credits.

2. **Vector Store Issues**:

If the vector store fails to load, delete the vectorstore/ directory and restart the app to recreate it.

3. **Model Not Responding**:
For Llama3, ensure that Ollama is running locally and the model is downloaded:

```
ollama pull llama3
ollama serve
```