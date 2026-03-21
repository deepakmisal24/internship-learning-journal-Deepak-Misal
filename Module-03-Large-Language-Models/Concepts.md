# **📘 Course Documentation: Module 3 – Large Language Models**

## **1. LLM (Large Language Model)**

An LLM is a very advanced computer program trained on a massive amount of text (books, websites, code). It works like a super-powered "autocomplete." Based on the words you give it, it predicts what words should come next.

*    Example: When you ask an LLM to "Write a poem about a cat," it uses the patterns it learned from millions of other poems to generate something new.

## **2. LLM Agents**

A standard LLM just talks. An Agent is an LLM that can do things. You give it a goal and a set of "tools" (like a calculator or a web browser), and it decides which tool to use to finish the job.

*    Example: An agent tasked with "Research the weather in Paris and email my boss" would use a weather tool, summarize the data, and then use an email tool.

## **3. LLM vs. Chatbot**

*    LLM: The "brain." It’s the underlying engine (like GPT-4 or Claude).

*    Chatbot: The "body" or the interface you talk to (like ChatGPT or Gemini). A chatbot uses an LLM to generate its answers but also has extra features like a memory of your past messages.

## **4. LLM Sentiment Analysis**

This is using an LLM to figure out the "vibe" or emotion of a piece of text.

*    Example: If you feed the LLM 1,000 product reviews, it can instantly tell you which ones are happy (Positive), angry (Negative), or indifferent (Neutral).

## **5. LLM Structured Extraction**

LLMs usually give you messy paragraphs. Structured Extraction is forcing the LLM to pull specific facts out of a text and put them into a clean format like a table or a JSON list.

*    Example: Giving the AI a messy medical bill and asking it to extract only the "Date," "Hospital Name," and "Total Amount."

## **6. Base64 Encoding**

Computers talk in numbers, but humans talk in letters. Base64 is a way to turn "binary data" (like an image or a PDF) into a long string of text. This is useful because LLM APIs often prefer receiving data as text strings rather than raw files.

## **7. Prompt Engineering**

This is the "art" of writing the best possible instructions for an AI. It’s about being specific.

*    Bad Prompt: "Write about dogs."

*    Good Prompt: "Act as a veterinarian and write a 200-word informative guide for new Golden Retriever owners about diet."

## **8. Prompt Refining & Optimization**

This is the process of trial and error. You try a prompt, see where the AI got confused, and rewrite the prompt to fix those mistakes. It's like coaching an employee until they get the task exactly right.

## **9. Response Model**

In programming, a Response Model defines the "shape" of the answer you expect. It tells the AI: "Don't just talk; I need your answer to have exactly three fields: Name, Age, and City."

## **10. API End-point**

An API is a way for two computers to talk to each other. The End-point is like a specific phone number for a service.

*    Example: To get an answer from OpenAI, your code "calls" a specific URL (the end-point) and sends your prompt.

## **11. Open-Meteo**

This is a popular, free Weather API. In data science projects, we often use it to teach LLMs how to look up real-time weather information since LLMs don't "know" the current weather on their own.

## **12. Tokenization & Prompt Tokens**

LLMs don't read words; they read Tokens (chunks of characters).

*    Tokenization: The act of chopping text into these chunks.

*    Prompt Tokens: The "cost" of your input. If your prompt is 10 words, it might be 13 tokens. You usually pay AI companies per token.

## **13. Pydantic & Pydantic AI**

*    Pydantic: A Python tool that checks if data is "valid." (e.g., Is "Age" actually a number and not a word?)

*    Pydantic AI: A new framework that uses Pydantic specifically for AI. It makes sure that when an LLM gives an answer, it fits perfectly into your code without breaking anything.

## **14. Embedding & Multimodal Embedding**

*    Embedding: Turning a word or sentence into a long list of numbers (a vector). Similar meanings get similar numbers.

*    Multimodal Embedding: Doing the same for images and sounds. This allows a computer to "know" that a picture of a dog and the word "puppy" are related because their numbers are close together.

## **15. Vector Database**

A special type of storage for Embeddings. Unlike a regular database that searches for exact words, a Vector Database searches for meaning. It can find "fruit" even if you only typed "apple."

## **16. RAG (Retrieval-Augmented Generation)**

LLMs have a "cutoff date" for their knowledge. RAG solves this. When you ask a question, the system first looks through your own private documents (Retrieval), finds the relevant pages, and gives them to the LLM to read before it answers (Generation).

*    Example: A chatbot that knows your specific company's HR policy.

## **17. Hybrid RAG**

This combines the "Meaning" search (Vector search) with "Keyword" search (Traditional search). It ensures you get the best of both worlds—understanding the context while also finding specific names or serial numbers.

## **18. Multimodal Capabilities**

This means the AI can handle more than just text. It can "see" images, "hear" audio, and "speak" back.

## **19. Vision Models**

These are LLMs that can analyze images.

*    Example: You upload a photo of your fridge, and the Vision Model tells you: "You have eggs, milk, and spinach. You could make an omelet."

## **20. LLM Image and Speech Generation**

*    Image Generation: Creating a picture from a description (like DALL-E or Midjourney).

*    Speech Generation: Turning text into a realistic human voice.

## **21. Function Calling**

This is when an LLM realizes it can't answer a question on its own and "calls" a piece of code to do it.

*    Example: You ask "What is 1,234×5,678?" Instead of guessing the math, the LLM uses Function Calling to run a Python calculator and gives you the exact answer.