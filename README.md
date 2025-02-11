# SmartNews

# News RAG Chatbot

This project collects news articles from CNN, summarizes them, and uses a Retrieval-Augmented Generation (RAG) approach to build a chatbot. The chatbot answers queries using real news context.

## How It Works

The project involves several key steps:

1. **News Collection**  
   - **Scraping:** The `news_collection.py` script uses the `newspaper3k` library to scrape articles from CNN.  
   - **Saving:** Each article is saved in the `data/` directory along with its title, URL, publish date, and full content.

2. **Summarization**  
   - **Filtering:** Articles are checked for language, size, and irrelevant content.  
   - **Extractive Summarization:** An extractive summary is generated using a TF-IDF based method.  
   - **Saving Summaries:** Summaries are saved in the `summarized_data/` directory.

3. **Embedding & Retrieval (RAG Component)**  
   - **Embedding:** All news articles (or their summaries) are converted into vector embeddings using the Sentence Transformer model `all-MiniLM-L6-v2`.  
   - **Indexing:** A FAISS index is built from these embeddings for fast similarity searches.  
   - **Retrieval:** When a user query is submitted, the system retrieves the most relevant articles by comparing the query's embedding with the stored vectors.  
   - *This retrieval process forms the "R" (Retrieval) part of RAG.*

4. **Chatbot with LLM (RAG Component)**  
   - **LLM Used:** The generative model (by default, **GPT-2 Medium**) is used as the LLM. (You can replace this with a more powerful model such as GPT-Neo-2.7B if needed.)  
   - **Prompt Construction:** A prompt is built by combining the retrieved news context with the user's query.  
   - **Response Generation:** The LLM generates a response based on the prompt.  
   - *This LLM-based response generation constitutes the "G" (Generation) part of the Retrieval-Augmented Generation (RAG) approach.*

5. **Scheduled Updates**  
   - **Automation:** The scheduler (using APScheduler) periodically runs the news collection and summarization process to keep the dataset updated.

## Setup Instructions

1. **Install Dependencies:**
   ```bash
   pip install newspaper3k nltk faiss-cpu sentence-transformers transformers scikit-learn apscheduler langid
