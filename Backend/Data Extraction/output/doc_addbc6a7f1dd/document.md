<image-ref id="doc_addbc6a7f1dd_image_000001" />

# YouTube Video Summarization & Q&A with RAG

AI-Powered, Context-Aware Summaries Using Transformer Models

Presented by: Vishnu Vardhan Reddy Alla, valla1@mtu.edu

Advisor: Keith Vertanen, vertanen@mtu.edu

# The Problem (Introduction):

Over 500 hours of videos are uploaded to YouTube every minute.

Viewers often struggle to extract key information from lengthy videos.

·

Manual skimming is inefficient and time-consuming.

There's a growing demand for:

o Concise, high-quality summaries

o Accurate answers to specific user queries

# The Solution (Objective):

Automatically generate summaries for YouTube videos.

Provide precise answers to user-defined questions.

Utilize Retrieval-Augmented Generation (RAG) to enhance contextual relevance.

# · Leverage:

Transformer-based language models

Vector embeddings for efficient information retrieval

# Experiment settings:

Summarization: Models are evaluated at different temperature values for response variability and coherence.

Q & A: tested using top K (number of chunks retrieved) and Cosine threshold (filters relevant content based on similarity score).

<image-ref id="doc_addbc6a7f1dd_image_000002" />

# Key takeaways:

GPT-4 mini & GPT-3.5 Turbo lead in Q&A, with BERT scores > 0.90 at higher K values.

Claude Sonnet shows stable performance across temperatures, maintaining ~0.85 BERT scores.

As K increases the performance also increases consistently for all models and there is no particular trend for cosine threshold.

# Models Evaluated:

<table-ref id="doc_addbc6a7f1dd_table_000001" />

| Model         | Type        |   Temper atue | K       |   Cosine Threshold |   BERT Score (Summarization) BERT (K) (Q |   Score &A) BERT Score (Cosine) (Q &A) |
|:--------------|:------------|--------------:|:--------|-------------------:|-----------------------------------------:|---------------------------------------:|
| GPT-3.5 Turbo | Chat Model  |           0.3 | 10 0.75 |            0.84255 |                                  0.90962 |                                0.90832 |
| GPT-4 mini    | Chat Model  |           0.2 | 10 0.5  |            0.8502  |                                  0.91264 |                                0.91298 |
| DeepSeek R1   | Open Source |           0.3 | 6 0.55  |            0.83842 |                                  0.87879 |                                0.88085 |
| Claude Sonnet | Chat Model  |           0.8 | 10 0.65 |            0.85093 |                                  0.88595 |                                0.89147 |
| Claude Haiku  | Chat Model  |           0.5 | 10 0.6  |            0.84664 |                                  0.88073 |                                0.88341 |
| DeepSeek V3   | Open Source |           0.6 | 8 0.45  |            0.83845 |                                  0.87785 |                                0.87754 |

Dataset: ClarityClips/youtube-video-summarization (Hugging Face). Q&A Benchmark: Manually curated synthetic dataset.

Metric: BERTScore for evaluating relevance and quality.

<table-ref id="doc_addbc6a7f1dd_table_000002" />

| 0           | 1         |
|:------------|:----------|
| BERT Score  | Inference |
| 1 - 0.95    | Excellent |
| 0.94 - 0.85 | Very Good |
| 0.84 - 0.7  | Good      |
| 0.69 - 0.5  | Fair      |

# Conclusion:

This experiment demonstrates the effectiveness of combining RetrievalAugmented Generation (RAG) with transformer-based models for summarizing and querying YouTube videos. Fine-tuning retrieval parameters like topK and cosine similarity significantly enhances Q&A performance. Stable summarization is achievable through careful temperature control, while retrieval thresholds influence both efficiency and accuracy.

# Reference:

Retrieval-Augmented Generation for Knowledge-Intensive NLP TasksPatrick Lewis, Ethan Perez, Aleksandra Piktus, et al.arXiv preprint arXiv:2005.11401 (2020)

BERTScore: Evaluating Text Generation with BERTTianyi Zhang, Varsha Kishore, Felix Wu, et al.arXiv preprint arXiv:1904.09675 (2019).

Document Q&A with ChromaDB - Google Generative AI Documentation.

# How it works (Method Overview):

Transcript Extraction: Fetching video transcripts using the YouTube API.

Chunking + Embeddings: Splitting transcripts into manageable chunks and converting the chunks into vector representations using embeddings.

· ChromaDB: Storing vectors in a local vector database for effectively retrieving the most relevant chunks for a query.

Transformer Models: Using large language models to summarize the video content and generate answers to user questions.

<image-ref id="doc_addbc6a7f1dd_image_000003" />