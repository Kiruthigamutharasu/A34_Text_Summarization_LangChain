# Text Summarization using LangChain

## Overview

In this assignment, I implemented different text summarization techniques using LangChain and a locally running LLM through Ollama.  
The main goal was to understand how different summarization strategies behave when working with small and large documents, rather than just generating summaries.

I experimented with four approaches:

- Prompt-based summarization
- Stuff Chain
- Map-Reduce Chain
- Refine Chain

Instead of focusing only on output, I tried to observe how each method performs in terms of execution time, scalability, and summary quality.

---

## Dataset Used

For this project, I used a long research-style PDF document so that chunking and long-document handling could be tested properly.

The document was intentionally large to understand how LangChain manages token limits and multi-step summarization workflows.

---

## Technologies Used

- Python 3.11 (Virtual Environment)
- LangChain (latest version)
- LangChain Classic (for legacy summarization chains)
- Ollama (local LLM execution)
- llama3.2:1b model
- Jupyter Notebook

I used a local model instead of cloud APIs so the entire project could run without paid resources.

---

## Implementation Approach

### 1. Prompt-Based Summarization
I first started with a simple prompt template where the document text was directly sent to the model.  
This helped me understand how much control prompting gives over the output style.

### 2. Stuff Chain
Next, I implemented the stuff chain which sends the entire document in one request.  
It worked well for smaller inputs but struggled once the document size increased.

### 3. Map-Reduce Chain
This approach divided the document into smaller chunks, summarized each chunk individually, and then combined the results.  
This method handled large inputs better but required significantly more processing time.

### 4. Refine Chain
In this method, the summary was gradually improved as new chunks were processed.  
I noticed that this produced more coherent summaries compared to map-reduce.

---

## Challenges I Faced

This assignment involved more debugging than I initially expected.

### 1. LangChain Version Changes
Many examples available online used older imports which no longer work in the latest LangChain versions.  
I had to figure out new import paths such as `langchain_community`, `langchain_text_splitters`, and `langchain_classic`.

### 2. Ollama Model Issues
At first, my code failed because the model name I used was not installed locally.  
I learned that Ollama requires pulling models manually before they can be accessed from Python.

### 3. Extremely Long Execution Time
When I initially ran the Map-Reduce chain, the notebook kept running for more than 15 minutes.  
Later I realized that the document was split into nearly 200 chunks, which meant hundreds of LLM calls were being executed sequentially.  
I reduced the number of chunks to make experimentation practical.

### 4. Tokenizer Dependency Error
During the reduce phase, LangChain required a tokenizer for token counting and threw an error related to the `transformers` package.  
Installing the dependency fixed the issue, but it took some time to understand why it was needed.

### 5. Understanding Trade-offs
Another challenge was realizing that better summaries usually required more computation time.  
Initially I assumed slower execution meant something was broken, but it was actually part of how the algorithms work.

---

## Key Observations

From my experimentation:

- Prompt-based summarization is simple but not scalable.
- Stuff chain is fast but limited by input size.
- Map-reduce handles large documents reliably but is slower.
- Refine chain produces more coherent summaries but requires multiple iterations.

I understood that choosing a summarization method depends heavily on document size and available computation resources.

---

## How to Run the Project

1. Create Python 3.11 virtual environment
2. Install dependencies:
pip install -r requirements.txt

3. Run Jupyter Notebook and execute cells sequentially.

---

## Final Thoughts

While starting this assignment, I expected it to be mostly about writing prompts, but I ended up learning more about practical LLM workflows, debugging environment issues, and handling large documents efficiently.

Working with a local LLM also helped me understand real-world limitations like latency and resource constraints, which are usually hidden when using cloud APIs.

Overall, this assignment helped me move from theoretical understanding to practical implementation.