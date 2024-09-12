# btechfinalyearproject
SIT 2021-2025 FINAL Year Project

# Description

This project aims to automate the process of performing literature reviews on research papers using Natural Language Processing (NLP) techniques and Large Language Models (LLMs). The tool extracts and summarizes key information from research papers in PDF format, such as the title, author, year, findings, results, and limitations, providing a quick and structured overview of the paper.

Key Features:
- PDF Parsing: Converts research papers in PDF format into machine-readable text.
- Core NLP Techniques: Uses Regular Expressions (Regex) and Named Entity Recognition (NER) to identify and extract key elements like Title, Author, Year, and more.
- LLM-based Extraction: Employs advanced models like Retrieval-Augmented Generation (RAG) and Prompt Engineering to extract meaningful content from sections like Abstract, Conclusion, and user-provided problem statements.
- Automated Insights: Generates summaries for Findings, Results, and Limitations based on the document content and user queries.
- Structured Output: Organizes the extracted data into a structured format, making it easier for users to review multiple papers efficiently.

# Workflow

<img width="440" alt="image" src="https://github.com/user-attachments/assets/8852b673-b8e3-405c-a96c-6a1822198f8d">

PDF Document Submission: A user uploads a research paper in PDF format that needs to be analyzed.

Parsing the PDF: The system converts the PDF into a machine-readable text format, breaking down its content into sections like Title, Authors, Abstract, and Conclusion.

Preprocessing the Content: Basic text cleaning, such as removing unnecessary characters or handling formatting issues, takes place. The document is now ready for extraction.

Entity and Structure Extraction (Core NLP): Using techniques like Regex and Named Entity Recognition (NER), the system identifies key entities such as the Title, Author, and Year of 
publication from the text that appears before the abstract. It segments different sections like Abstract (for Findings), Conclusion (for Results), and combines the user-provided problem statement and Conclusion for extracting Limitations.

Language Model Processing (LLM - RAG and Prompt Engineering): The system uses a Retrieval-Augmented Generation (RAG) model to pull relevant data from the research paper and fine-tune the answers using Prompt Engineering. This step generates meaningful insights, such as summarizing the findings, results, and limitations.

Output Generation: The system processes all the extracted data into structured output, like Title, Author, Year, Findings, Results, and Limitations, providing a clean summary.

# Cloud Architecture

<img width="426" alt="image" src="https://github.com/user-attachments/assets/6ab85427-34ee-491c-b0b5-603b4a3ef970">

1. User Inputs PDF and Query: The user uploads a PDF document and enters a query (e.g., "What are the results and limitations of this paper?") through the Frontend Application (hosted on Azure 
Static Web Apps or Web App Service).

2. PDF Parses Through Azure Function: Upon PDF upload, an Azure Function is triggered to handle the document parsing. It uses a library (e.g., pdfplumber, PyMuPDF) to convert the PDF content into a machine-readable format (plain text).
This parsing process extracts the raw content of the PDF and organizes it for further processing.

3. Parsed Data is Stored in Azure Blob Storage: After parsing, the extracted text (or structured data) is stored in Azure Blob Storage. This acts as the central repository for parsed documents.
The Blob Storage is connected to the Azure API Management (APIM) service, enabling API-based interaction between the storage and downstream services.
Via APIM, User Query and Parsed Data Go to Azure Machine Learning for Text Analytics (Regex, NER, LLM: RAG, and Prompt Engineering):

4. Azure API Management (APIM) serves as the gateway. It collects the user’s query and the parsed data from Blob Storage.
APIM passes this data to Azure Machine Learning (AML) for advanced text analytics: Regex and NER (Named Entity Recognition) extract key elements like title, author, and year. The RAG model retrieves relevant information (such as abstract or conclusion) and uses Prompt Engineering to generate coherent answers to the user query (e.g., extracting "Findings," "Results," and "Limitations").

5. Output is Returned to APIM: The processed output from Azure Machine Learning (containing answers to the user’s query) is returned back to APIM. APIM formats the response and sends it back to the Frontend Application for user access.

6. Output is Stored in Azure SQL Database or Cosmos DB: The final structured output (title, author, findings, results, limitations, etc.) is stored in Azure SQL Database or Azure Cosmos DB for easy retrieval and future queries. This ensures that the extracted information is persistently stored and can be referenced without re-processing the original document.
