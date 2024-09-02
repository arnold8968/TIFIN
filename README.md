# RAG-Based QA System for Investment Insights

## Objective
This project aims to build a robust Question-Answering system using Retrieval-Augmented Generation techniques. The goal is to accurately process and retrieve information from the Investment Case For Disruptive Innovation.pdf and provide well-grounded answers. The focus is on leveraging Natural Language Processing (NLP) and Large Language Models (LLMs) to handle the document's complex layout and generate relevant responses. Given the intricate structure, the system needs to efficiently ingest the document, retrieve relevant content, and synthesize answers based solely on the provided information. Since the evaluation questions don't come with predefined answers, I manually extracted the ground truth answers from the PDF.


## Project Structure

### 1. Data Preparation


Extract textual content from PDF documents while preserving the structure and quality.

Tools: Various Python libraries like pdfminer, PyMuPDF, and pdfplumber were evaluated to determine which tool best maintains text integrity.

Chart Handling: Recognizing the potential issues with extracting text from charts and tables, layout analysis tools were employed to separate these elements from the main text. Although the process of using GPT to describe chart meanings and store them in a database was initiated, it remains incomplete.

Post-Processing: Implemented techniques to clean and refine the extracted text, ensuring the removal of any unwanted characters or extraction artifacts.


### 2. Vector Database
   
Embedding Model: all-MiniLM-L6-v2

Objective: Convert extracted text into vector embeddings for efficient similarity search.

Model: The all-MiniLM-L6-v2 embedding model was selected for its balance between performance and computational efficiency.

Vector Storage: The Chroma vector database was used to store these embeddings, facilitating rapid similarity searches for the RAG process.



### 3. RAG_LLM

Effective prompt engineering was applied to ensure the model receives clear instructions, allowing it to think through the problem and break down complex tasks. This approach improves the quality of the generated responses.

- The prompt structure is tested in the playground and follows clear instructions:
  - Give the model time to think.
  - Break down complex tasks.
  - Format the answer output.

Different Models


1. **Basic LLaMA**: Asks the question without any related content.
2. **RAG LLaMA**: Uses vector database to calculate similarity and adds the content into the prompt.
3. **RAG Rerank LLaMA**: (Brief explanation of how it works included in the notebook)

- For better comparison, all outputs are saved into a dataset.

### 4.Evaluation


Metrics Used:


Average BLEU Score: Assesses the precision of the generated responses.

Average ROUGE-L Score: Evaluates the relevance and recall by comparing the longest matching subsequence between the generated answers and the ground truth.

Benchmarking: The system was tested against 20 questions from Evaluation_Questions.txt. Since the questions lacked predefined answers, I manually located the correct answers in the PDF to use as ground truth for evaluation.



### 5.Benchmarking

Evaluation Questions: The system's performance was benchmarked using the 20 provided questions, comparing the results of both baseline and advanced RAG methods.

Performance Comparison: Documented the improvements achieved by the advanced methods over the baseline approach.



# Analysis of Sample Outputs

Example
Question: What is the core objective of investing in disruptive innovation according to ARK?

This question is summary and should be answered based on the entire text.

My GT:
The core objective of investing in disruptive innovation, according to ARK, is to capitalize on companies that are at the forefront of developing technologies capable of displacing older technologies or creating entirely new markets. ARK seeks to provide exposure to these innovative companies, aiming for long-term growth by investing in firms driving disruptive innovation across various sectors.

Basic LLM:
The core objective of investing in disruptive innovation according to ARK is to identify and capitalize on the potential of new technologies and business models that have the ability to transform entire industries and create significant value for investors. ARK's investment strategy is focused on identifying and investing in companies that are at the forefront of innovation and disruption, with the goal of generating long-term capital appreciation for its clients.

RAG_LLM:
The core objective of investing in disruptive innovation according to ARK is to offer investors access to companies at the forefront of technology-enabled innovation, in some of the most promising areas of the economy, with potential for long-term growth.

RAG_Rerank:
ARK's main goal in investing in disruptive innovation is to focus on companies that are creating new technologies or replacing outdated ones, with the hope of achieving long-term growth by supporting these leading innovators.








