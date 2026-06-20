# Resume RAG Assistant

## Overview

This project implements a simple RAG system that allows users to ask questions about a resume and receive context-aware answers.

The goal is to understand the complete RAG pipeline, including document processing, embedding generation, semantic retrieval, and LLM-based answer generation.

---
## Architecture
```
             Resume PDF
                  |
                  ↓
          Document Extraction
            (PDF → Text)
                  |
                  ↓
          Document Cleaning
     (Fix PDF formatting issues)
                  |
                  ↓
               Chunking
        (Split text into pieces)
                  |
                  ↓
              Embedding
           (Text → Vector)
                  |
                  ↓
          Similarity Search
         (Find relevant chunks)
                  |
                  ↓
                Prompt
                  |
                  ↓
                 LLM
                  |
                  ↓
                Answer
```
---
### 1. Document Loading
Problem: The computer can not read content in pdf files directly.

Solution: PDF → Text

### 2. Cleaning
Problem: In the PDF, the format and structure seem good. But in the machine, it displays like "P y t h o n"

Solution: fix format.

### 3. Chunking
Problem: LLM Context Window is limited. For example, we can not send 100 pages pdf files to GPT directly.

Solution:
```
Document
↓
Chunk1
Chunk2
Chunk3
```

### 4. Embedding
Problem: Computer can not understande whether the meaning of 'vacation' and 'annual leave' is similar or not.

Solution: Transfer text to vector
```
Python
↓
[0.23,0.45,...]
```

### 5. Retrieval
Problem: Not sure the question is related to which chunk.

Solution: Calculate Question vector vs Document vectors, find the most similar content.

### 6.Generation
Problem:搜索结果只是资料，不是答案。

Solution:LLM-Relevant information + Question = Natural language answer


你这次项目学到的核心概念
1. RAG不是训练模型
这是最重要的。
很多初学者误解：

给我的简历训练一个GPT

实际上：
没有训练。
只是：
外部知识
+
检索
+
LLM

---

2. Embedding不是关键词搜索
错误理解：
Python → 找Python

正确：
语义空间距离

所以：
Programming skills
≈
Big Data Analytics

是可能的。

---

3. 数据质量决定RAG效果
你亲自遇到了：
PDF:
Python

变成：
P y t h o n

导致：
Retrieval失败。
所以：
Garbage in
Garbage out

---

如果面试让你解释这个项目
不要说：

I used SentenceTransformer and cosine similarity.

太像教程。
应该说：

I built a simple RAG pipeline for resume question answering. I first extracted and cleaned PDF text, split documents into chunks, converted them into embeddings, retrieved relevant chunks based on semantic similarity, and finally used an LLM to generate answers based on retrieved information.

这就是工程描述。

---

你现在的位置
如果把RAG学习分阶段：
Level 0
Python基础
      ↓
Level 1
调用LLM API
      ↓
Level 2
理解RAG pipeline   ← 你现在这里
      ↓
Level 3
使用LangChain/LlamaIndex
      ↓
Level 4
Vector DB
(Qdrant, Chroma)
      ↓
Level 5
Evaluation
(RAGAS, reranking)
      ↓
Level 6
Production RAG
(Cloud, API, monitoring)
