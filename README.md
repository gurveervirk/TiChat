# TiChat

<div align="center">
  <img height="400" width="400" alt="gurveervirk/TiChat" src="https://github.com/gurveervirk/TiChat/blob/main/app/public/TiChat.png">
</div>

This project is a *Simple*, *high quality*, *ChatGPT-esque*, *extensible RAG application*, that makes use of AI models and indices to query documents and retrieve better-informed responses from the models. It allows you to upload your documents that can be used to answer any corresponding queries. It automatically stores your chats for future usage.

A sample online implementation of this project is available [here](https://github.com/gurveervirk/BlenderHelperBot-with-TiDB).

## Prerequisites

This app has a single dependency that needs to be installed separately:
- [Ollama](https://ollama.com/download) for quick and easy model download, serving as well as automatic and smart device loading

This app makes use of TiDB vector store. For quick setup, head over to [TiDB Cloud](https://tidbcloud.com/) and sign up for a free account.

Get the connection string for your database (default: 'test'), after generating the password. Also, download the CA certificate to your system.

## Getting Started

1) Go to the Releases page, and download the latest TiChatInstaller.exe. 
2) Run it and follow the steps to complete the installation.
3) Go to the installation directory (default: "C:\Program Files (x86)\TiChat"), and make the following changes to settings.json:
    - *connectionString* to the connection string for your TiDB cloud account, with ssl_ca = full path to your installed CA cert

**Done! You can now run the application.**

## Usage

Start the app from desktop or start menu after completing the above tasks.

The app allows the user to simply chat with the bot, if the checkbox is left unchecked, or use the index created with the uploaded documents for better-informed responses.

Upload documents using the top right button.

This is how it should look like:

<div align="center">
  <img alt="gurveervirk/TiChat" src="https://github.com/gurveervirk/TiChat/blob/main/misc/ui.png">
</div>

## Application Explained

### Components:
1) **Ollama (Local LLM Runtime)**:
  - Hosts the local LLM model (**Mistral-7B-Instruct-v0.3**).
  - Runs inference locally for generating responses based on prompts.
2) **FastEmbedEmbedding (ONNX Model)**:
  - Runs locally on the CPU.
  - Generates vector embeddings from text data (e.g., document uploads).
  - Model: **mixedbread-ai/mxbai-embed-large-v1**.
3) **TiDB (Vector Store)**:
  - A distributed, scalable vector database that stores the embeddings.
  - Provides vector search capabilities.
4) **Llama-Index (Vector Index)**:
  - Interface layer between the application and TiDB.
  - Manages vector indexes and performs efficient retrieval for relevant documents.
5) **RAG Chatbot Application**:
  - The main user interface where users interact with the chatbot.
  - Orchestrates the flow of data between different components.

Frontend has been built using **React** and **Bootstrap 5**.

### Data Flow:

<div align="center">
  <img alt="gurveervirk/TiChat" src="https://github.com/gurveervirk/TiChat/blob/main/misc/diagram.png">
</div>

There are 2 main flows:
1) If the user does not use the index, it directly calls the LLM, like a normal chatbot app.
2) If the user checks '_Use Index Querying_', the following occurs:
- _User Input_: The user inputs a query via the chatbot interface.
- _Embedding Generation_: The query is passed to the FastEmbedEmbedding ONNX model to generate its vector embedding. The question, along with the previous messages, is condensed into a single question for better response.
- _Vector Search_: The generated embedding is sent to Llama-Index, which queries TiDB for relevant document embeddings. TiDB returns the most relevant document vectors.
- _Contextual Response Generation_: The retrieved documents (in their original text form) are provided as context to the LLM model in Ollama. The LLM generates a response based on the query and the retrieved documents.
- _Response Delivery_: The generated response is displayed to the user through the chatbot interface.
