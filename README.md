# RAG-Based QA System for Investment Insights

## Objective
This project aims to build a robust Question-Answering system using Retrieval-Augmented Generation techniques. The goal is to accurately process and retrieve information from the Investment Case For Disruptive Innovation.pdf and provide well-grounded answers. The focus is on leveraging Natural Language Processing (NLP) and Large Language Models (LLMs) to handle the document's complex layout and generate relevant responses. Given the intricate structure, the system needs to efficiently ingest the document, retrieve relevant content, and synthesize answers based solely on the provided information. Since the evaluation questions don't come with predefined answers, I manually extracted the ground truth answers from the PDF.


## Project Structure

### 1. Data Preparation


Extract textual content from PDF documents while preserving the structure and quality.

Tools: Various Python libraries like pdfminer, PyMuPDF, and pdfplumber were evaluated to determine which tool best maintains text integrity.

Chart Handling: Recognizing the challenges of extracting meaningful text from charts and tables, we employed layout analysis tools to separate these elements from the main text. The next step involves using GPT to interpret and describe the chart content, which will then be stored in a database. However, this task is still in progress and hasn't been completed yet.

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

Result: The RAG_Rerank approach significantly enhanced the relevance of the retrieved content in response to the questions. By implementing reranking, the model was able to prioritize and select the most pertinent information from the initial retrieval set, leading to more accurate and contextually appropriate answers. This improvement in content relevance directly contributed to a noticeable increase in the overall accuracy of the generated responses compared to the baseline and standard RAG methods.

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



Compare Retrieval Content:

pdf_info: PDF source: Investment Case For Disruptive Innovation.pdf. Source from 17 pages. 
 Content: ARK Seeks to Capture Disruptive Innovation
The ARK Innovation ETF (ARKK) Aims to Offer
1 Access to Growth  Investors who seek to access companies at the forefront of technology-enabled innovation, in some of the most  promising areas of the economy, with potential for long-term growth.
2 Portfolio Diversification Potentially Suited for investors who like to diversify their existing portfolio with strategies that offer low correlation to a  number of core asset classes held in most investors’ portfolios.
3 Moderate-to-High Risk-Reward Profile A constant focus on secular changes and disruptive innovation can compliment traditional strategies and core portfolios  May be suited for investors who have a moderate-to-high risk profile and intend to stay invested for the medium-to-long  term.
The information herein is general in nature and should not be considered financial advice An investor should consult a financial professional regarding the investor’s specific situation Diversification does not assure a profit.

pdf_info: PDF source: Investment Case For Disruptive Innovation.pdf. Source from 20 pages. 
 Content: ARK Innovation ETFs
Thematic Strategies Focused on Disruptive Innovation 
ARKK ARK Innovation ETF
ARKX ARK Space Exploration & Innovation ETF
ARKW ARK Next Generation Internet ETF 
PRNT The 3D Printing ETF
ARKQ ARK Autonomous Tech & Robotics ETF 
IZRL Israel Innovative Technology ETF
ARKG ARK Genomic Revolution ETF 
ARKF ARK Fintech Innovation ETF

pdf_info: PDF source: Investment Case For Disruptive Innovation.pdf. Source from 2 pages. 
 Content: D I S C L O S U R E
Risks of Investing in Innovation
Please note: Companies that ARK believes are capitalizing on disruptive innovation and developing technologies to displace older technologies or create new markets 
may not in fact do so ARK aims to educate investors and seeks to size the potential investment opportunity, noting that risks and uncertainties may impact our 
projections and research models Investors should use the content presented for informational purposes only, and be aware of market risk, disruptive innovation risk, 
regulatory risk, and risks related to certain innovation areas 
Please read risk disclosure carefully.
RISK OF INVESTING IN INNOVATION
RAPID PACE OF CHANGE
REGULATORY HURDLES
EXPOSURE ACROSS SECTORS AND MARKET CAP
DISRUPTIVE  INNOVATION
POLITICAL OR LEGAL PRESSURE
UNCERTAINTY AND UNKNOWNS 
COMPETITIVE LANDSCAPE
à    Aim for a cross-sector understanding of technology    and combine top-down and bottom-up research.
à    Aim to understand the regulatory, market, sector,         and company risks (See Disclosure Page)
Sources: ARK Investment Management LLC, 2023.



Rerank content:

pdf_info: PDF source: Investment Case For Disruptive Innovation.pdf. Source from 17 pages. 
Content: ARK Seeks to Capture Disruptive Innovation
The ARK Innovation ETF (ARKK) Aims to Offer
1 Access to Growth  Investors who seek to access companies at the forefront of technology-enabled innovation, in some of the most  promising areas of the economy, with potential for long-term growth.
2 Portfolio Diversification Potentially Suited for investors who like to diversify their existing portfolio with strategies that offer low correlation to a  number of core asset classes held in most investors’ portfolios.
3 Moderate-to-High Risk-Reward Profile A constant focus on secular changes and disruptive innovation can compliment traditional strategies and core portfolios  May be suited for investors who have a moderate-to-high risk profile and intend to stay invested for the medium-to-long  term.
The information herein is general in nature and should not be considered financial advice An investor should consult a financial professional regarding the investor’s specific situation Diversification does not assure a profit.

pdf_info: PDF source: Investment Case For Disruptive Innovation.pdf. Source from 18 pages. 
Content: ARK Seeks to Capture Disruptive Innovation
5 Reasons Investors Should Consider ARKK
1 Exposure To Innovation: Aims for thematic multi-cap exposure to innovation across sectors ARK believes the securities held in 
ARKK present the best risk-reward opportunities from ARK’s innovation-based themes.
2 Growth Potential: Aims to capture long-term growth with low correlation of relative returns to traditional growth strategies and 
negative correlation to value strategies 
3 Tool For Diversification1: Offers a tool for diversification due to little overlap with traditional indices It can be a complement to 
traditional value/growth strategies 
4 Grounded In Research: Combines top-down and bottom-up research in its portfolio management to identify innovative companies 
and convergence across markets.
5 Cost Effective: Seeks to provide a lower cost alternative to mutual funds with true active management in an exchange traded fund 
(ETF) that invests in rapidly moving themes.
[1] Diversification does not assure a profit The information herein is general in nature and should not be considered financial advice An investor should consult a financial professional regarding the investor’s specific situation.

pdf_info: PDF source: Investment Case For Disruptive Innovation.pdf. Source from 22 pages. 
Content: Disclosures
Investors  should  carefully  consider  the  investment  objectives  and  risks  as  well  as  charges  and  expenses  of  an  ARK  ETF  before  investing  This  and  other  information are contained in the ARK ETFs’ prospectuses, which may be obtained by visiting www.ark-funds.com The prospectus should be read carefully  before investing 
Investing in securities involves risk and there's no guarantee of principal.
Fund Risks: The principal risks of investing in the ARKK include: Equity Securities Risk The value of the equity securities the Fund holds may fall due to general market and economic conditions Foreign Securities Risk  Investments in the securities of foreign issuers involve risks beyond those associated with investments in U.S securities Health Care Sector Risk The health care sector may be adversely affected by government regulations  and government health care programs Communications Sector Risk Companies is this sector may be adversely affected by potential obsolescence of products/services, pricing competition, research and development costs,  substantial capital requirements and government regulation Information Technology Sector Risk Information technology companies face intense competition, both domestically and internationally, which may have an  adverse  effect  on  profit  margins  Additional  risks  of  investing  in  ARKK  include  equity,  market,  management  and  non-diversification  risks,  as  well  as  fluctuations  in  market  value  and  NAV  Disruptive  Innovation  Risk  Companies that ARK believes are capitalizing on disruptive innovation and developing technologies to displace older technologies or create new markets may not in fact do so Companies that initially develop a  novel  technology  may  not  be  able  to  capitalize  on  the  technology  Companies  that  develop  disruptive  technologies  may  face  political  or  legal  attacks  from  competitors,  industry  groups  or  local  and  national  governments  These  companies  may  also  be  exposed  to  risks  applicable  to  sectors  other  than  the  disruptive  innovation  theme  for  which  they  are  chosen,  and  the  securities  issued  by  these  companies  may  underperform the securities of other companies that are primarily focused on a particular theme 
The Fund’s exposure to cryptocurrency may change over time and, accordingly, such exposure may not always be represented in the Fund’s portfolio Many significant aspects of the U.S federal income tax treatment of  investments in bitcoin are uncertain and an investment in bitcoin may produce income that is not treated as qualifying income for purposes of the income test applicable to regulated investment companies, such as the  Fund GBTC is expected to be treated as a grantor trust for U.S federal income tax purposes, and therefore an investment by the Fund in GBTC will generally be treated as a direct investment in bitcoin for such purposes See  ‘‘Taxes’’ in the Fund’s SAI for more information 
An investment in an ETF is subject to risks and you can lose money on your investment in an ETF There can be no assurance that the ETF will achieve its investment objective The ETF’s portfolio is more volatile than broad  market averages Shares of ARKK are bought and sold at market price (not NAV) and are not individually redeemed from the ETF ETF shares may only be redeemed directly with the ETF at NAV by Authorized Participants, in  very large creation units There can be no guarantee that an active trading market for ETF shares will develop or be maintained, or that their listing will continue or remain unchanged Buying or selling ETF shares on an  exchange may require the payment of brokerage commissions and frequent trading may incur brokerage costs that detract significantly from investment returns.
Portfolio holdings will change and should not be considered as investment advice or a recommendation to buy, sell or hold any particular security Please visit www.ark-funds.com for the most current list of holdings for the  ARK ETFs.
The information herein is general


