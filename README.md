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

## How it works

1. **Memory chunk creation**: Chat histories are divided into fixed-sized "memory chunks" of 200 tokens, with an overlapping window approach to preserve context.

2. **Hierarchical memory structure**: Summarize every 5 consecutive memory chunks of one level (e.g., L1 memories) into a more abstract representation called a higher-level memory (e.g., L2 memories). The process is repeated for higher levels, with 5 L2 memories summarized into an L3 memory, and so on.

3. **Utilizing ChatGPT API for summarization**: The ChatGPT API is used to create summaries for higher-level memories, with the LLM accessing the memory vectorstore to provide improved context during the summarization process.

4. **Storing memory chunks**: Each memory chunk is stored in a vectorstore without a specific structure, with metadata attached to each memory chunk, including its level number (e.g., L1, L2) and references to the lower-level chunks it represents.

5. **Maintaining all levels of memory chunks in the vectorstore**: The LLM retrieves information at different levels of abstraction based on user queries, enabling access to both specific and abstract information.

6. **Updating the hierarchical structure**: During chatting, the system checks if the latest 5 L1 memories are summarized or not. If not, they are summarized to create an L2 memory. This process continues for higher levels as necessary, always checking if 5 consecutive memories of a certain level are summarized before creating a higher-level memory.

7. **Retrieval process**: When a user provides a prompt, a similarity search is performed with the prompt to retrieve relevant memories from the vectorstore, regardless of their level of abstraction. The top result from vector similarity is assumed to provide the best context. If the context window allows for more tokens, additional relevant memories can be included to provide a more comprehensive response.

## Installation

(TBA)

## Usage

(TBA)

## Contributing

(TBA)

## License

(TBA)

