# 📘 Module 3: Compiled Learnings — Large Language Models

This documentation summarizes the core concepts, architectures, and deployment strategies for working with Large Language Models (LLMs) as covered in Week 3.

---

## 🧠 1. Foundational Architecture

### **LLM (Large Language Model)**
The core engine trained on massive datasets to predict the next "token" in a sequence. It acts as a sophisticated pattern-matching machine rather than a factual database.

### **Tokenization & Cost**
* **Tokenization:** The process of breaking text into chunks (tokens) for the model to process.
* **Prompt Tokens:** Your input (the "question").
* **Completion Tokens:** The model's output (the "answer").
* **Significance:** APIs charge based on total token count.



### **LLM vs. Chatbot**
* **LLM:** The raw model (e.g., GPT-4, Claude 3.5).
* **Chatbot:** The product wrapper (e.g., ChatGPT) that manages UI, safety filters, and conversation history.

---

## 🛠️ 2. Data Extraction & Logic

### **LLM Structured Extraction**
The process of instructing an LLM to parse unstructured text (like an email or receipt) and return a clean **JSON** object.

### **Base64 Encoding**
A method of converting binary data (like images) into a text string. This is essential for sending visual data to an LLM via a standard **API End-point**.

### **LLM Sentiment Analysis**
Automated classification of text into emotional categories (Positive, Negative, Neutral) to gauge user feedback at scale.

---

## 🎯 3. Prompting & Validation

### **Prompt Engineering & Optimization**
The iterative process of designing, testing, and refining instructions to make model responses more **robust** and accurate.

### **Response Model & Pydantic AI**
* **Response Model:** A Pydantic class that defines the exact structure an AI must follow.
* **Pydantic AI:** A framework that ensures "Type-Safety," preventing the AI from returning data that might crash your application.
* **Pydantic vs. Pydantic AI:** Pydantic handles general data validation; Pydantic AI handles the specific orchestration of LLM instructions and tools.



---

## 🔍 4. Knowledge Retrieval (RAG)

### **Embeddings & Vector Databases**
* **Embedding:** Converting text into numerical vectors representing **meaning**.
* **Vector Database:** A specialized storage system that retrieves information based on semantic similarity rather than exact keywords.



### **RAG (Retrieval-Augmented Generation)**
A technique that allows an LLM to "read" your private documents before answering, effectively giving the model an "Open Book Exam" to prevent hallucinations.

### **Hybrid RAG**
Combines **Vector Search** (semantic) with **Keyword Search** (exact) to ensure accuracy for specific names, dates, or serial numbers.



---

## 🤖 5. Agents & Multimodal Workflows

### **LLM Agents**
An autonomous system that uses a **ReAct loop** (Reasoning + Action) to decide which **Tools** to use to accomplish a complex goal.

### **Function Calling**
The mechanism that allows an LLM to request the execution of a specific piece of code (e.g., calling the **Open-Meteo API** to get real-time weather data).



### **Multimodal Capabilities**
* **Vision Models:** Models that can interpret visual data (images/charts).
* **Speech Generation:** Converting AI-generated text into natural-sounding human speech.