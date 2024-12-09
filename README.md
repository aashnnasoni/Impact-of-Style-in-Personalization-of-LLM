# Personalized News Headline Generation using LLM-Based RAG Pipeline

This project implements a hybrid Retrieval-Augmented Generation (RAG) pipeline to generate personalized news headlines. By combining style embeddings and dense retrieval, the pipeline creates tailored outputs based on user profiles and article content, outperforming traditional retrieval methods like BM25.

## Overview  
The pipeline leverages two retrieval phases and combines their results to maximize relevance and personalization. These retrieved articles serve as context for a language model to generate the final headlines.

---

## Pipeline Details  

### **Pipeline 1: Style Embedding-Based Retrieval**  
This phase retrieves the top-k articles using stylistic patterns from user profiles:  
1. **Style Embedding Extraction:** Utilized Wegmann et al. (2022)’s model to extract style embeddings from user profile documents.  
2. **Embedding Averaging:** Computed the average embedding to represent overall stylistic tendencies.  
3. **Cosine Similarity Ranking:** Ranked profile documents by cosine similarity to the average embedding.  
4. **Top-k Retrieval:** Retrieved the top-k documents as candidates.

### **Pipeline 2: Dense Retrieval Using FAISS**  
This phase retrieves articles based on semantic similarity:  
1. **Query Variants Generation:** Used the Gemini Flash 1.5 LLM to generate \( k \) query variants from the original query.  
2. **Dense Retrieval with FAISS:** Indexed documents using FAISS for efficient similarity search, retrieving the top-k most relevant documents.

### **Generation Phase**  
1. **Hybrid Context Construction:** Combined results from both pipelines to form a union of top-2k retrieved articles.  
2. **Headline Generation:** Fed the expanded context into Flan-T5 (base) to generate personalized news headlines.

---

## Results and Evaluation  
The hybrid approach was compared against individual retrieval pipelines and baseline models (e.g., BM25). Results demonstrated superior performance:  
- **Rouge-1 Score:** 0.0985  
- **Rouge-L Score:** 0.0894  

The hybrid method effectively balanced stylistic preferences and semantic relevance, making it the most effective approach.

---

## Key Features  
- **Hybrid Retrieval Approach:** Combines style embeddings and dense retrieval for personalized context.  
- **Efficient Search:** Leverages FAISS for scalable and efficient dense retrieval.  
- **State-of-the-Art Models:** Integrates Wegmann et al.'s style embedding model, Gemini Flash 1.5, and Flan-T5.  
- **Baseline Comparisons:** Benchmarked performance against BM25 and individual retrieval pipelines.

---

## Future Work  
- Enhance the style embedding model for better stylistic matching.  
- Experiment with larger LLMs for improved headline generation.  
- Extend support for multilingual headline generation.

---

This project showcases the potential of hybrid RAG pipelines in addressing personalization challenges in generative tasks, paving the way for future innovations in retrieval-augmented systems.
