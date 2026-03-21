# 📁 Data Sourcing & Web Engineering: The Fundamentals

This guide covers the journey from identifying a data source to automating the extraction process using modern libraries and cloud tools.

---

## 🏗️ 1. Core Concepts (The Basics)

### **Data Sourcing (Definition)**
Data Sourcing is the process of identifying and gathering raw information from various locations (databases, social media, sensors, or websites) to solve a specific problem.
* **Simple Explanation:** It is like a chef deciding which farms to buy ingredients from before they start cooking. Without a high-quality "source," the final analysis will be flawed.

### **Web Crawling**
A "Crawler" (or Spider) is a program that browses the internet automatically. It starts at one webpage, finds all the links on that page, and follows them to new pages, mapping out the web.
* **Simple Explanation:** Imagine a robot that enters a library and its only job is to find every "See Also" note in a book and immediately run to that next book to find even more notes. This is how Google search works.

### **Web Scraping**
While crawling *finds* pages, **Scraping** *extracts* specific data from them. It involves reading the HTML code of a site and pulling out only the pieces you need (like prices, movie titles, or dates).
* **Simple Explanation:** If the internet is a wall of posters, a "Crawler" finds where the posters are, but a "Scraper" is you standing there with a notebook writing down only the phone numbers from those posters.

---

## 🛠️ 2. The Scraping Toolkit

To scrape effectively, we use different libraries depending on the complexity of the website.

| Library | Role | The Analogy |
| :--- | :--- | :--- |
| **Requests** | Data Retrieval | **The Phone Call:** It asks the server for the HTML code and brings it back to you. |
| **BeautifulSoup4** | HTML Parsing | **The Highlighter:** It helps you find specific tags (like `<h1>` or `<a>`) in a messy pile of code. |
| **Playwright** | Browser Automation | **The Remote Control:** It opens a real browser and "clicks" buttons or "scrolls" like a human. |

### **Specialized High-Speed Tools**
* **HTTPX:** A faster, modern version of `requests` that can handle multiple tasks at the same time (Asynchronous).
* **LXML:** An industrial-strength parser. If BeautifulSoup is a highlighter, LXML is a high-speed professional scanner—it reads thousands of lines of code in milliseconds.

---

## 🤖 3. Modern & Advanced Scraping

### **Using LLMs for Web Scraping**
Instead of writing complex code to find specific HTML tags, we give the raw code to an AI (like Gemini or GPT). 
* **Concept:** You simply tell the AI, "Find the product name and price in this text," and the AI understands the context to extract it perfectly, even if the website layout changes.
* **Simple Explanation:** Instead of you searching for a needle in a haystack, you give the haystack to a super-smart robot and say, "Find the needle."

### **Video Scraping**
Video scraping involves extracting data *from* video files or their metadata. 
* **How it works:** This can include downloading the video, extracting the captions/transcript, or using AI to detect what objects (like cars or people) appear in specific frames.
* **Simple Explanation:** It’s like having a computer watch 1,000 hours of YouTube and writing down every time a specific person speaks or a specific product appears.

---

## ⏰ 4. Scheduled Scraping (Automation)

Usually, scraping only happens when you manually press "Run." **GitHub Actions** allows us to automate this.

### **The Workflow**
1. **The Trigger:** You set a "Cron" timer (e.g., "Run every day at 8:00 AM").
2. **The Environment:** GitHub wakes up a virtual computer (a runner).
3. **The Execution:** The runner installs your libraries (`httpx`, `lxml`), runs your script, and saves the data.
4. **The Storage:** GitHub can automatically "Commit" the new data (CSV/JSON) back into your folder.

---

## 📈 Summary Comparison

| Goal | Best Tool |
| :--- | :--- |
| **Simple text from a site** | Requests + BeautifulSoup |
| **Clicking buttons/Logging in** | Playwright |
| **Massive data speed** | HTTPX + LXML |
| **Messy, unstructured data** | LLM Extraction |
| **Daily price tracking** | GitHub Actions |