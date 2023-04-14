<p align="center">
  <img src=".well-known/logo-nobg.png" alt="Pira" width="40%" />
</p>

# Pyramind: Hierarchical Memory Recall System for Language Models

This repository contains the implementation of a Hierarchical Memory Recall System for Language Models (LLMs), such as ChatGPT. The aim of this project is to enhance the memory recall capabilities of LLMs by organizing chat histories into a hierarchical structure with varying levels of abstraction.

## Features

- Memory chunk creation
- Hierarchical memory structure
- Utilizing ChatGPT API for summarization
- Storing memory chunks with metadata
- Maintaining all levels of memory chunks in the vectorstore
- Updating the hierarchical structure during chatting
- Retrieval process based on similarity search

## Quickstart (largely from [chatgpt-retrieval-plugin]<https://github.com/openai/chatgpt-retrieval-plugin>)

Follow these steps to quickly set up and run the ChatGPT Retrieval Plugin:

1. Install Python 3.10, if not already installed.
2. Clone the repository: `git clone https://github.com/leo4life2/hierarchical_memory_plugin.git`
3. Navigate to the cloned repository directory: `cd /path/to/hierarchical_memory_plugin`
4. Install poetry: `pip install poetry`
5. Create a new virtual environment with Python 3.10: `poetry env use python3.10`
6. Activate the virtual environment: `poetry shell`
7. Install app dependencies: `poetry install`
8. Rename `.env.example` to `.env`, and set the required environment variables (make sure you have a Pinecone account and index created).
9. Run `source .env` to load the environment variables.
10. Run the API locally: `poetry run start`
11. Access the API documentation at `http://0.0.0.0:8000/docs` and test the API endpoints (make sure to add your bearer token).

## How it works

1. **Memory chunk creation**: Chat histories are divided into fixed-sized "memory chunks" of 200 tokens, with an overlapping window approach to preserve context.

2. **Hierarchical memory structure**: Summarize every 5 consecutive memory chunks of one level (e.g., L1 memories) into a more abstract representation called a higher-level memory (e.g., L2 memories). The process is repeated for higher levels, with 5 L2 memories summarized into an L3 memory, and so on.

3. **Utilizing ChatGPT API for summarization**: The ChatGPT API is used to create summaries for higher-level memories, with the LLM accessing the memory vectorstore to provide improved context during the summarization process.

4. **Storing memory chunks**: Each memory chunk is stored in a vectorstore without a specific structure, with metadata attached to each memory chunk, including its level number (e.g., L1, L2) and references to the lower-level chunks it represents.

5. **Maintaining all levels of memory chunks in the vectorstore**: The LLM retrieves information at different levels of abstraction based on user queries, enabling access to both specific and abstract information.

6. **Updating the hierarchical structure**: During chatting, the system checks if the latest 5 L1 memories are summarized or not. If not, they are summarized to create an L2 memory. This process continues for higher levels as necessary, always checking if 5 consecutive memories of a certain level are summarized before creating a higher-level memory.

7. **Retrieval process**: When a user provides a prompt, a similarity search is performed with the prompt to retrieve relevant memories from the vectorstore, regardless of their level of abstraction. The top result from vector similarity is assumed to provide the best context. If the context window allows for more tokens, additional relevant memories can be included to provide a more comprehensive response.

## Usage

With the Pyramind plugin enabled, ChatGPT will try to proactively remember dialogues it considers important, but of course, you can also inform it to remember things you want it to. The Pyramind plugin organizes chat histories into a hierarchical structure with varying levels of abstraction, allowing ChatGPT to retrieve information at different levels of abstraction based on user queries, enabling access to both specific and abstract information.

## Supported Vector Databases

This repo is largely based on the [chatgpt-retrieval-plugin](https://github.com/openai/chatgpt-retrieval-plugin) repo, and all the vector databases it supports should work here, but it currently has only been tested on the Pinecone vectorstore.
