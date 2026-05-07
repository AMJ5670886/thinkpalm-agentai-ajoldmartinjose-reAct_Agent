# thinkpalm-agentai-ajoldmartinjose-reAct_Agent
AJOLD MARTIN JOSE
Lab 1 — ReAct Agent
Build a minimal Python ReAct agent that: takes a user query → reasons step-by-step → calls a tool → returns final answer. Run in Google Colab. Screenshot your working output.

## Overview

This project demonstrates a ReAct agent designed to find information about films using the TMDB API. It allows users to query film details, including director, cast, year, and language, and is configured for secure API key management in Google Colab.

## Structure

- `/src`: Contains the main Python script for the film agent.
- `/screenshots`: Stores any visual outputs or demonstration images.
- `README.md`: This file, providing project information.

## How to Run

1.  **Clone the Repository**:
    ```bash
    git clone <your-repo-url>
    cd <your-repo-name>
    ```

2.  **Set up Google Colab (Recommended)**:
    *   Open the original `.ipynb` file in Google Colab.
    *   **API Keys**: This project requires API keys for Groq and TMDB. Go to the 'Secrets' tab (key icon on the left sidebar in Colab) and add the following secrets:
        *   `GROQ_API_KEY`: Your API key from Groq.
        *   `TMDB_API_KEY`: Your API key from TMDB.
    *   Run all cells in the Colab notebook.

3.  **Run Locally (Advanced)**:
    *   **Install Dependencies**:
        ```bash
        pip install -r requirements.txt
        ```
    *   **API Keys**: Set your `GROQ_API_KEY` and `TMDB_API_KEY` as environment variables.
        ```bash
        export GROQ_API_KEY="your_groq_api_key"
        export TMDB_API_KEY="your_tmdb_api_key"
        ```
    *   Run the main script:
        ```bash
        python src/film_agent.py
        ```

## Tools Used

-   **Groq API**: For generating agent responses using `llama-3.1-8b-instant`.
-   **The Movie Database (TMDB) API**: For searching and retrieving film information.
-   **`requests`**: Python library for making HTTP requests to external APIs.
-   **`openai`**: Python client for interacting with the Groq API (which uses OpenAI-compatible API). 
-   **`re`**: Python module for regular expressions.
-   **`json`**: Python module for JSON parsing.
