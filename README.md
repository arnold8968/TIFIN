# RAG-Based QA System for Investment Insights

## Objective
This project aims to build a robust Question-Answering system using Retrieval-Augmented Generation techniques. The goal is to accurately process and retrieve information from the Investment Case For Disruptive Innovation.pdf and provide well-grounded answers. The focus is on leveraging Natural Language Processing (NLP) and Large Language Models (LLMs) to handle the document's complex layout and generate relevant responses. Given the intricate structure, the system needs to efficiently ingest the document, retrieve relevant content, and synthesize answers based solely on the provided information. Since the evaluation questions don't come with predefined answers, I manually extracted the ground truth answers from the PDF.


## Project Structure

1. Data Preparation
Text Extraction from PDFs
Objective: Extract textual content from PDF documents while preserving the structure and quality.
Tools: Various Python libraries like pdfminer, PyMuPDF, and pdfplumber were evaluated to determine which tool best maintains text integrity.
Chart Handling: Recognizing the potential issues with extracting text from charts and tables, layout analysis tools were employed to separate these elements from the main text. Although the process of using GPT to describe chart meanings and store them in a database was initiated, it remains incomplete.
Post-Processing: Implemented techniques to clean and refine the extracted text, ensuring the removal of any unwanted characters or extraction artifacts.


3. Document Ingestion
Text Extraction: I used Python libraries like pdfminer, PyMuPDF, and pdfplumber to extract text from the PDF. Given the limited computation resources available on Colab, I conducted sample testing on a random selection of 5 PDFs.
Handling Non-Text Elements: Charts and tables were separated using layout analysis tools. Although I began work on using GPT to interpret these elements and store them in a database, this part is still a work in progress.
Post-Processing: The extracted text underwent a cleanup process to remove any artifacts and ensure the data was ready for further processing.
4. Vector Database
Embedding Model: I used the all-MiniLM-L6-v2 model to convert the processed text into vector embeddings.
Vector Storage: The embeddings were stored in a Chroma vector database, enabling efficient similarity searches, which are crucial for the RAG system.
5. Retrieval-Augmented Generation (RAG) with LLM
Prompt Engineering: Crafted prompts to guide the model in providing clear, well-structured answers. The prompts were tested in a playground environment to refine their effectiveness. Key strategies included:
Allowing the model time to think.
Breaking down complex tasks into manageable steps.
Formatting the output for clarity.
Model Variants:
Basic LLaMA: Answers questions without additional context.
RAG LLaMA: Incorporates relevant content from the vector database into the prompt.
RAG Rerank LLaMA: Further refines the RAG LLaMA by reranking retrieved results, ensuring the most relevant content is prioritized.
Output Documentation: All generated answers were stored in a dataset for comparison and analysis.
6. Evaluation
Metrics Used:
Average BLEU Score: Assesses the precision of the generated responses.
Average ROUGE-L Score: Evaluates the relevance and recall by comparing the longest matching subsequence between the generated answers and the ground truth.
Benchmarking: The system was tested against 20 questions from Evaluation_Questions.txt. Since the questions lacked predefined answers, I manually located the correct answers in the PDF to use as ground truth for evaluation.
7. Benchmarking
Evaluation Questions: The system's performance was benchmarked using the 20 provided questions, comparing the results of both baseline and advanced RAG methods.
Performance Comparison: Documented the improvements achieved by the advanced methods over the baseline approach.
