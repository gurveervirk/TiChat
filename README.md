# TiChat

<div align="center">
  <img height="400" width="400" alt="gurveervirk/ToK" src="https://github.com/gurveervirk/TiChat/blob/main/app/public/TiChat.png">
</div>

This project is a *Simple*, *high quality*, *ChatGPT-esque*, *extensible RAG application*, that makes use of AI models and indices to query documents and retrieve better-informed responses from the models. It allows you to upload your documents that can be used to answer any corresponding queries. It automatically stores your chats for future usage.

## Prerequisites

This app has a single dependency that needs to be installed separately:
- [Ollama](https://ollama.com/download) for quick and easy model download, serving as well as automatic and smart device loading

This app makes use of TiDB vector store. For quick setup, head over to [TiDB Cloud](https://tidbcloud.com/) and sign up for a free account.

Get the connection string for your database (default: 'test'), after generating the password. Also, download the CA certificate to your system.

## Getting Started

1) Go to the Releases page, and download the latest TiChatInstaller.exe. 
2) Run it and follow the steps to complete the installation.
3) Go to the installation directory (default: "C:\Program Files (x86)\ToK"), and make the following changes to settings.json:
    - *connectionString* to the connection string for your TiDB cloud account, with ssl_ca = full path to your installed CA cert

**Done! You can now run the application.**

## Usage

Start the app from desktop or start menu after completing the above tasks.

The app allows the user to simply chat with the bot, if the checkbox is left unchecked, or use the index created with the uploaded documents for better-informed responses.

Upload documents using the top right button.
