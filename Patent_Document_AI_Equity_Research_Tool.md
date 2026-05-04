# PATENT / INVENTION DISCLOSURE DOCUMENT

---

## 1. Title

**AI-Powered Equity Research Analysis Tool Using Retrieval-Augmented Generation with Dynamic Web Scraping, Semantic Vector Indexing, and Interactive Natural Language Querying**

---

## 2. Field of Invention

The present invention relates generally to the field of **Artificial Intelligence (AI) applied to financial technology (FinTech)**, and more particularly to a system and method for automated equity research analysis. The invention pertains to the convergence of multiple technical domains including:

- **Natural Language Processing (NLP)** for understanding and generating human-readable financial insights from unstructured web content.
- **Web Scraping and Content Extraction** using hybrid static and dynamic rendering techniques for obtaining financial data from publicly accessible websites.
- **Vector Embedding and Semantic Search** for converting unstructured textual data into high-dimensional mathematical representations that enable meaning-based retrieval.
- **Retrieval-Augmented Generation (RAG)** as an AI architecture that grounds Large Language Model (LLM) responses in factual, retrieved document content to minimize hallucinations.
- **Interactive Data Visualization and Export** for generating charts, graphs, and Excel spreadsheets directly from analyzed financial data through natural language commands.

The invention is situated at the intersection of computational finance, information retrieval, generative AI, and human-computer interaction, specifically targeting the automation and augmentation of equity research workflows used by financial analysts, portfolio managers, retail investors, and academic researchers.

---

## 3. Background of the Invention

### 3.1 State of the Art in Equity Research

Equity research is a critical function in the financial services industry, involving the systematic analysis of publicly traded companies, their financial health, market position, competitive landscape, and growth prospects. Traditionally, this process has been heavily reliant on manual effort—analysts spend considerable time reading through financial reports (10-K, 10-Q filings), earnings call transcripts, news articles, market commentary, and various online sources such as Yahoo Finance, Moneycontrol, Zerodha Varsity, Bloomberg, and other financial data platforms.

The conventional workflow typically involves:

1. **Manual Source Identification**: Analysts manually identify and navigate to relevant web pages, PDF documents, and data portals to gather information about specific stocks, sectors, or market events.
2. **Manual Data Extraction**: Key financial metrics (market capitalization, P/E ratio, revenue, debt-to-equity ratios) are manually copied from web pages into spreadsheets or note-taking tools.
3. **Manual Summarization**: Analysts write summaries, investment thesis documents, and research notes by hand after reading through multiple sources, a process that can take hours to days.
4. **Static Tooling**: Existing tools such as Excel, PDF viewers, and terminal-based platforms provide no conversational interface and require analysts to formulate specific data queries rather than asking natural language questions.

### 3.2 Limitations of Existing Systems

Current systems and methods for equity research suffer from several significant drawbacks:

- **Time-Intensive Processes**: Reading and synthesizing information from 10–50 web pages for a single stock analysis can take several hours, reducing the number of companies an analyst can cover.
- **No Unified Multi-Source Analysis**: There is no mechanism to automatically combine and cross-reference information from multiple URLs into a single, coherent knowledge base.
- **Lack of Conversational Interfaces**: Analysts cannot ask follow-up questions about the data they have collected without manually re-reading source documents.
- **Static and Disconnected Tools**: Traditional tools (Excel, PDF readers, note-taking apps) do not communicate with each other, requiring manual data transfer between stages of the research workflow.
- **Inability to Handle Dynamic Web Content**: Many modern financial websites (such as NSE India, interactive chart pages, and single-page applications) rely heavily on JavaScript rendering, which simple HTTP-based scraping tools cannot handle.
- **Hallucination in AI Tools**: General-purpose AI chatbots (such as ChatGPT or Gemini) can generate plausible but factually incorrect financial data because they are not grounded in the specific documents the analyst is reviewing.
- **No Automated Visualization from Context**: Existing systems do not offer the ability to generate custom charts and export structured Excel files directly from analyzed content using natural language commands.

### 3.3 Evolution of Relevant Technologies

The development of transformer-based language models (BERT, GPT, LLaMA) has fundamentally changed text understanding capabilities. Financial-domain variants such as FinBERT have shown improved performance in sentiment analysis and entity extraction from financial texts. Concurrently, vector databases like Pinecone, Weaviate, and ChromaDB have enabled efficient semantic similarity search over millions of document embeddings. The emergence of the Retrieval-Augmented Generation (RAG) paradigm—first formalized by Lewis et al. (2020)—provides a principled way to combine retrieval from a knowledge base with generative language models, producing answers that are both fluent and factually grounded.

However, there remains a significant gap in the market for a system that seamlessly combines:
- Robust web scraping of both static and dynamic financial websites
- Real-time text optimization and embedding generation
- Persistent vector storage with semantic retrieval
- LLM-powered summarization and question answering grounded in user-supplied documents
- Automated chart generation and Excel export from analyzed data
- A unified, conversational user interface for all of the above

The present invention addresses this gap comprehensively.

---

## 4. Objects of the Invention

The primary objects of the present invention are:

1. **To provide an automated system** for scraping, extracting, and processing financial content from multiple publicly accessible web URLs, handling both static HTML pages and JavaScript-rendered dynamic web applications through a hybrid scraping mechanism.

2. **To implement a Retrieval-Augmented Generation (RAG) pipeline** that converts unstructured financial web content into structured vector embeddings, stores them in a scalable vector database, and uses them to generate accurate, context-grounded responses to user queries.

3. **To eliminate hallucination in AI-generated financial insights** by ensuring that all generated summaries, answers, and analyses are exclusively derived from the user-supplied source documents retrieved from the vector store, rather than from the language model's pre-trained knowledge.

4. **To provide an interactive conversational interface** (chatbot) that allows users—including financial analysts, investors, and students—to query their indexed financial content using natural language, with full conversation history support for contextual follow-up questions.

5. **To automate the generation of executive summaries** from multi-source financial content, highlighting key metrics, company profiles, risk factors, and notable data points, thereby reducing the time required for manual summarization from hours to seconds.

6. **To enable automated data visualization** by allowing users to request charts, graphs, and visual representations of financial data through natural language commands, with the system generating executable Python code (using Matplotlib) from the analyzed content and returning rendered images.

7. **To support automated Excel/spreadsheet generation** from analyzed financial data, enabling users to export structured tabular data directly from the chatbot interface without manual data entry.

8. **To implement a secure, multi-user authentication system** with email-based OTP verification and JWT token management, ensuring that the platform can be deployed as a multi-tenant SaaS application.

9. **To provide a scalable, modular architecture** that separates concerns across frontend (React.js), backend API (FastAPI), vector storage (Pinecone), AI inference (Groq/LLaMA), and embedding generation (HuggingFace), enabling independent scaling and future extension of each component.

10. **To create a foundation for future enhancements** including speech-to-text input for voice-based research queries, real-time market data integration, and multi-language support for global equity research.

---

## 5. Summary of the Invention

The present invention discloses a system and method for AI-powered equity research analysis that automates the end-to-end pipeline from financial web content ingestion to interactive, grounded, and intelligent analysis. The system is composed of a multi-layer architecture involving a React.js-based frontend, a Python/FastAPI-based backend, a Pinecone vector database for semantic storage, and a Groq-hosted LLaMA large language model for generation tasks.

### System Overview

The invention operates through a multi-stage pipeline architecture that automates the complete equity research workflow from data ingestion to interactive analysis. Each stage is described below.

### 5.1 URL Ingestion and Web Scraping
The user provides one or more publicly accessible finance-related URLs (e.g., company pages on Moneycontrol, Yahoo Finance, Zerodha, or financial news articles) through a web-based interface. The backend receives these URLs and initiates a hybrid scraping process. First, a static extraction is attempted using HTTP requests with appropriate headers and the Trafilatura library for main content extraction, with BeautifulSoup as a fallback parser. If static extraction fails (common with JavaScript-heavy single-page applications), the system automatically falls back to Playwright-based dynamic rendering, which launches a headless Chromium browser to fully render the page before extracting content.

### 5.2 Text Optimization
The raw extracted text is passed through an LLM-based optimization step that cleans formatting issues (e.g., separating labels from values that appear on different lines), removes navigation boilerplate, advertisements, and footer text, and restructures the content into a dense, information-rich format optimized for semantic search retrieval.

### 5.3 Chunking and Embedding
The optimized text is split into manageable chunks (1500 characters with 200-character overlap) using a recursive character text splitter. Each chunk is converted into a 768-dimensional vector embedding using a remote HuggingFace embedding model hosted on Hugging Face Spaces.

### 5.4 Vector Indexing
The generated embeddings, along with their associated text metadata, are upserted into a dynamically created Pinecone serverless index (AWS us-east-1, cosine similarity metric). Each analysis session creates a unique index, enabling isolated and concurrent multi-user operations.

### 5.5 Summary Generation
Simultaneously, the optimized text is passed to a Groq-hosted LLaMA 3.1 model which generates a concise, professional executive summary highlighting company profiles, key metrics, risk factors, and notable points.

### 5.6 Interactive Question Answering
Users can ask natural language questions through a chatbot interface. Each question is embedded into the same vector space, used to retrieve the top-5 most relevant document chunks from Pinecone via cosine similarity search, and then passed as context to the LLM along with conversation history. The LLM generates answers strictly grounded in the retrieved context, explicitly stating when information is not available in the indexed documents.

### 5.7 Automated Visualization
Users can request charts and graphs through natural language (e.g., "Show me a bar chart of market cap for these companies"). The system classifies the intent, retrieves relevant data via the RAG pipeline, generates executable Matplotlib Python code through the LLM, executes it in a sandboxed environment, and returns the rendered chart as a base64-encoded image.

### 5.8 Automated Excel Export
Similarly, users can request tabular data exports. The system generates structured JSON data through the LLM, converts it into a Pandas DataFrame, and exports it as a downloadable .xlsx file.

### 5.9 Security and Resilience
The system includes API key-based authorization, Groq API key rotation with failover for resilience, and CORS-enabled cross-origin access for frontend-backend communication. The modular design allows each component to be independently deployed, scaled, and updated.

---

## 6. Detailed Description

### 6.1 System Architecture

The system follows a four-layer architecture:

#### 6.1.1 Presentation Layer (Frontend)
The frontend is a React.js single-page application that provides:
- A URL input interface for submitting one or more finance-related web addresses
- A summary display panel that presents AI-generated executive summaries
- A tabbed chat interface with three modes: (a) General Q&A, (b) Visualization, and (c) Excel Export
- Real-time message rendering with support for text, images (base64-encoded charts), and downloadable Excel files
- Responsive design with auto-scrolling conversation view
- Token-based authentication with localStorage-persisted JWT tokens

The frontend communicates with the backend exclusively through RESTful HTTP API calls using Axios, sending JSON payloads and receiving structured JSON responses.

#### 6.1.2 Application Layer (Backend API)
The backend is implemented using FastAPI (Python) and exposes the following endpoints:

- **POST /register** — Initiates user registration by accepting a username and email, generating a 6-digit OTP, and sending it via the Brevo (formerly Sendinblue) transactional email API.
- **POST /verify-otp** — Verifies the OTP, hashes the user's password using bcrypt, and stores the credentials in MongoDB.
- **POST /login** — Authenticates with email/username and password, returning a signed JWT access token.
- **POST /analyze** — Accepts a list of URLs, triggers the scraping-embedding-indexing pipeline, and returns the dynamic index name and executive summary.
- **POST /ask** — Accepts a question and index name, performs semantic retrieval from Pinecone, and returns an LLM-generated answer grounded in the retrieved context.
- **POST /visuals** — Accepts a natural language visualization request, classifies intent, retrieves data, generates and executes Matplotlib code, and returns rendered chart images.
- **POST /excel** — Accepts a natural language data export request, classifies intent, generates structured data, and returns a base64-encoded Excel file.

CORS middleware is configured to allow cross-origin requests from all domains, enabling flexible frontend deployment.

#### 6.1.3 Data Layer
The data layer consists of two persistent stores:

- **Pinecone Vector Database**: Stores document chunk embeddings (768-dimensional vectors) with text metadata. Each user analysis session creates a unique serverless index (e.g., `webindex-a3f8b2c1`) with cosine similarity metric. The system manages index lifecycle, including automatic deletion of old indices when the 5-index free-tier limit is reached.
- **MongoDB (via Motor async driver)**: Stores user credentials (hashed passwords, email, username, OTP state) for the authentication system. The async Motor driver ensures non-blocking database operations compatible with FastAPI's async architecture.

#### 6.1.4 AI/Intelligence Layer
The AI layer comprises:

- **Remote Embedding Service**: A HuggingFace model deployed on Hugging Face Spaces, accessed via a custom REST API endpoint. It accepts batches of text strings and returns 768-dimensional embedding vectors. The `RemoteEmbeddingClient` class implements the LangChain `Embeddings` interface for seamless integration.
- **Groq-Hosted LLaMA Models**: The system uses Groq's inference infrastructure to access LLaMA 3.1 (8B Instant for summarization and Q&A) and LLaMA 3.3 (70B Versatile for code generation and complex reasoning). Multiple API keys are configured with random rotation and sequential failover for rate limit resilience.
- **RAG Pipeline**: The retrieval-augmented generation pipeline combines Pinecone semantic search (top-5 retrieval) with LLM context injection, ensuring that all generated content is grounded in the user's indexed documents.

### 6.2 Web Scraping Module (Detailed)

The scraping module implements a two-stage extraction strategy:

**Stage 1 — Static Extraction**:
- An HTTP GET request is made with browser-mimicking headers (User-Agent, Accept-Language, Accept).
- The response HTML is first processed by Trafilatura, a specialized library for main content extraction that intelligently strips navigation, sidebars, and boilerplate.
- If Trafilatura yields fewer than 200 characters, BeautifulSoup is used as a fallback to extract all text with newline separation.
- If both methods fail, the system proceeds to Stage 2.

**Stage 2 — Dynamic (JavaScript) Extraction**:
- Playwright launches a headless Chromium browser instance.
- The target URL is loaded with a `networkidle` wait strategy, ensuring all AJAX calls and dynamic rendering complete.
- The fully rendered HTML is then passed through the same Trafilatura → BeautifulSoup pipeline.
- This stage handles modern single-page applications built with React, Angular, or Vue that generate content client-side.

Both stages run asynchronously using `asyncio.to_thread()` to avoid blocking the FastAPI event loop. Multiple URLs are processed sequentially with per-URL results concatenated with source attribution headers.

### 6.3 Text Optimization Pipeline

Raw scraped text often contains formatting artifacts—labels and values on separate lines (e.g., "Market Cap\n1.34T"), navigation remnants, cookie consent text, and advertising copy. The optimization pipeline uses an LLM prompt to:
- Merge separated labels and values into key-value pairs (e.g., "Market Cap: 1.34T")
- Remove irrelevant boilerplate content
- Preserve all factual data, especially financial metrics, numbers, dates, and entity names
- Produce dense, structured text optimized for embedding quality and semantic retrieval precision

### 6.4 Embedding and Indexing Pipeline

The chunking strategy uses LangChain's `RecursiveCharacterTextSplitter` with a chunk size of 1500 characters and 200-character overlap. This ensures that:
- Each chunk contains sufficient context for meaningful embedding generation
- Overlap prevents information loss at chunk boundaries
- The recursive splitting strategy respects natural text boundaries (paragraphs, sentences) before falling back to character-level splits

Embeddings are generated in parallel batches (batch size 32) via the remote API. The resulting vectors are upserted to Pinecone with unique IDs combining document index and UUID fragments for deduplication safety.

### 6.5 Visualization Engine

The visualization subsystem implements a three-stage pipeline:
1. **Intent Classification**: An LLM classifier determines whether the user's message requests a visualization or is a general chat query.
2. **Code Generation**: For visualization requests, the RAG pipeline first retrieves relevant data, then an LLM generates executable Matplotlib Python code with strict rules for data fidelity (no hallucinated numbers), consistent units, proper figure sizing (12×7 inches), and readable formatting (rotated x-labels, tight layout, distinct colors).
3. **Sandboxed Execution**: The generated code is executed in a controlled namespace with only `matplotlib.pyplot` available. The resulting figure is saved to an in-memory buffer, encoded to base64, and returned to the frontend for inline display.

### 6.6 Excel Export Engine

The Excel export subsystem follows a similar pattern:
1. **Intent Classification**: Determines whether the user wants a spreadsheet or is chatting.
2. **Data Structuring**: The LLM generates a JSON array of objects representing table rows with appropriate column headers.
3. **DataFrame Conversion**: The JSON is converted to a Pandas DataFrame with cleaned column headers (stripped of Markdown formatting artifacts).
4. **Excel Generation**: The DataFrame is written to an in-memory Excel file using openpyxl, base64-encoded, and returned with a suggested filename.

### 6.7 Authentication System

The authentication system provides:
- **Registration**: Username + email → OTP sent via Brevo API → user record created in MongoDB with pending status.
- **OTP Verification**: 6-digit OTP validation → password hashing with bcrypt → user activation.
- **Login**: Email or username + password → bcrypt verification → JWT token issuance (HS256, configurable expiration defaulting to 24 hours).
- **Token Validation**: Bearer token in Authorization header, decoded and verified on protected endpoints.

### 6.8 Failover and Resilience Mechanisms

- **Multi-Key Groq API Rotation**: Up to 3 Groq API keys are configured. For each LLM call, keys are randomly shuffled and tried sequentially until one succeeds, providing resilience against individual key rate limits.
- **Scraping Fallback Chain**: Static → JavaScript rendering, ensuring content extraction from the widest range of websites.
- **Graceful Degradation**: If text optimization fails, the original text is used. If summary generation fails, a descriptive error message is returned rather than crashing the pipeline.
- **Pinecone Index Management**: Automatic deletion of the oldest index when the 5-index limit is reached, preventing creation failures.

---

## 7. Drawings

The following drawings and diagrams illustrate the system architecture and operational workflows:

### Drawing 1: System Architecture Diagram
A multi-layer architecture diagram showing:
- **User Layer**: Web browser accessing the React.js frontend
- **Frontend Layer**: React.js application hosted on Vercel, containing URL Input Module, Summary Display Module, Chat Interface Module (with Q&A, Visualization, and Excel tabs)
- **Backend Layer**: FastAPI server with endpoints (/analyze, /ask, /visuals, /excel, /register, /login, /verify-otp), hosted on Render/Hugging Face Spaces
- **Data Layer**: Pinecone Vector Database (serverless, AWS us-east-1) and MongoDB Atlas (user authentication data)
- **AI Layer**: HuggingFace Embedding Service (768-dim vectors) and Groq Inference API (LLaMA 3.1/3.3 models)
- **Arrows**: HTTPS communication between all layers, with labeled data flow directions

### Drawing 2: RAG Pipeline Flowchart
A detailed flowchart showing the complete Retrieval-Augmented Generation pipeline:
1. User submits URLs → 2. Hybrid Scraper (Static → JS fallback) → 3. Raw Text Extracted → 4. LLM Text Optimization → 5. Recursive Text Chunking (1500 chars, 200 overlap) → 6. Batch Embedding Generation (768-dim) → 7. Pinecone Upsert → 8. User Asks Question → 9. Question Embedding → 10. Top-5 Cosine Similarity Search → 11. Context + Question → LLM → 12. Grounded Answer Returned

### Drawing 3: Use Case Diagram
UML use case diagram with primary actor "Equity Research User" (analyst/investor/student) and use cases: Submit URLs, View Summaries, Ask Questions, Request Visualizations, Export Excel, Register/Login. System boundary encloses backend services.

### Drawing 4: Sequence Diagram — URL Processing Flow
Interaction between: User → React Frontend → FastAPI Backend → Playwright/BeautifulSoup → HuggingFace Embedding API → Pinecone → Groq LLM → React Frontend. Shows the temporal ordering of scraping, optimization, embedding, indexing, and summary generation.

### Drawing 5: Sequence Diagram — Question Answering Flow
Interaction between: User → React Frontend → FastAPI /ask → HuggingFace Embedding API → Pinecone Query → Groq LLM → React Frontend. Shows embedding of question, retrieval of top-k chunks, context-grounded answer generation.

### Drawing 6: State Chart Diagram — URL Processing Lifecycle
States: Received → Scraping (Static) → [Success/Fail] → Scraping (JS) → Parsing → Optimizing → Chunking → Embedding → Indexing → Completed / Failed. Shows transitions and decision points.

### Drawing 7: Deployment Diagram
Physical/virtual infrastructure mapping: User Device (Browser) ↔ Vercel (Frontend) ↔ Render/HF Spaces (FastAPI Backend) ↔ Pinecone Cloud (Vector DB) + MongoDB Atlas (Auth DB) + HuggingFace Spaces (Embedding API) + Groq Cloud (LLM Inference).

### Drawing 8: Visualization Generation Pipeline
Flowchart: User Request → Intent Classifier (viz/chat) → [If viz] RAG Data Retrieval → LLM Code Generation (Matplotlib) → Sandboxed Execution → Base64 Image Encoding → Frontend Rendering.

---

## 8. Abstract

The present invention provides a system and method for AI-powered equity research analysis that automates the extraction, processing, indexing, and intelligent querying of financial content from publicly accessible web sources. The system employs a hybrid web scraping mechanism combining static HTTP extraction (Trafilatura, BeautifulSoup) with dynamic JavaScript rendering (Playwright) to handle the full spectrum of modern financial websites. Extracted content undergoes LLM-based text optimization before being chunked and converted into 768-dimensional vector embeddings via a remote HuggingFace model, subsequently stored in a Pinecone serverless vector database for semantic similarity search.

The core of the invention is a Retrieval-Augmented Generation (RAG) pipeline that retrieves the most relevant document chunks for a given user query using cosine similarity and passes them as context to a Groq-hosted LLaMA large language model, producing accurate, grounded answers free from hallucination. The system further provides automated executive summary generation, natural language-driven data visualization (via dynamically generated and sandboxed Matplotlib code), and automated Excel spreadsheet export from analyzed content.

The invention is implemented as a web application with a React.js frontend and Python/FastAPI backend, includes a complete authentication system with email OTP verification and JWT tokens, and features multi-API-key failover for inference resilience. The modular architecture enables independent deployment and scaling of each component, making the system suitable for deployment as a scalable, multi-tenant SaaS platform for financial analysts, institutional investors, retail investors, and academic researchers.

---

## 9. Claims

**We claim:**

**Claim 1.** A computer-implemented system for automated equity research analysis comprising:
   (a) a hybrid web scraping module configured to extract textual content from one or more user-specified URLs using a first static extraction method and a second dynamic JavaScript-rendering extraction method, wherein the second method is invoked automatically upon failure of the first method;
   (b) a text optimization module that processes raw extracted text using a large language model to produce structured, dense, and information-rich text optimized for semantic search;
   (c) a chunking and embedding module that splits optimized text into overlapping segments and generates vector embeddings for each segment using a remote embedding model;
   (d) a vector storage module that stores the generated embeddings with associated text metadata in a cloud-based vector database supporting cosine similarity search;
   (e) a retrieval-augmented generation (RAG) module that, upon receiving a natural language query, embeds the query, retrieves the top-k most semantically similar document chunks from the vector database, and generates a context-grounded response using a large language model; and
   (f) a presentation module providing a web-based user interface for URL submission, summary display, conversational querying, visualization requests, and data export.

**Claim 2.** The system of Claim 1, wherein the hybrid web scraping module comprises:
   (a) a static extraction component that performs HTTP GET requests with browser-mimicking headers and extracts main content using the Trafilatura library, with BeautifulSoup as a fallback parser; and
   (b) a dynamic extraction component that launches a headless Chromium browser via Playwright, waits for network idle state, and extracts content from the fully rendered DOM.

**Claim 3.** The system of Claim 1, wherein the text optimization module uses a prompted large language model to:
   (a) merge label-value pairs separated by formatting artifacts into structured key-value pairs;
   (b) remove navigation elements, advertisements, cookie notices, and boilerplate content; and
   (c) preserve all factual data including financial metrics, dates, entity names, and numerical values.

**Claim 4.** The system of Claim 1, wherein the chunking and embedding module uses a recursive character text splitter with a configurable chunk size and overlap, and generates embeddings by transmitting text batches to a remotely hosted transformer-based embedding model via HTTP API calls.

**Claim 5.** The system of Claim 1, wherein the vector storage module dynamically creates a unique vector index for each analysis session, manages index lifecycle including automatic deletion of oldest indices when a configurable limit is reached, and uses a serverless cloud vector database with cosine similarity metric.

**Claim 6.** The system of Claim 1, further comprising an automated visualization module that:
   (a) classifies user intent to distinguish visualization requests from general conversational queries using a prompted large language model;
   (b) retrieves relevant data from the vector database via the RAG pipeline;
   (c) generates executable data visualization code (Matplotlib Python code) through a large language model with strict constraints against data fabrication;
   (d) executes the generated code in a sandboxed environment with restricted namespace; and
   (e) captures the rendered visualization, encodes it to base64 format, and transmits it to the presentation module for inline display.

**Claim 7.** The system of Claim 1, further comprising an automated data export module that:
   (a) classifies user intent to distinguish data export requests from general conversational queries;
   (b) generates structured tabular data in JSON format through a large language model grounded in retrieved document content;
   (c) converts the structured data into a spreadsheet format using a dataframe library; and
   (d) encodes the spreadsheet as a base64 string for client-side download.

**Claim 8.** The system of Claim 1, further comprising an authentication module that:
   (a) accepts user registration with username and email;
   (b) generates and transmits a one-time password (OTP) via transactional email API;
   (c) verifies the OTP, hashes the user's password using bcrypt, and stores credentials in a NoSQL database; and
   (d) issues JSON Web Tokens (JWT) upon successful authentication for session management.

**Claim 9.** The system of Claim 1, wherein the RAG module includes a multi-key failover mechanism that:
   (a) maintains a pool of multiple API keys for the large language model inference service;
   (b) randomly selects and attempts inference with a first key;
   (c) upon failure, sequentially attempts remaining keys in the pool; and
   (d) returns a graceful error message only when all keys in the pool have been exhausted.

**Claim 10.** A computer-implemented method for automated equity research analysis comprising the steps of:
   (a) receiving one or more URLs pointing to publicly accessible financial web content;
   (b) extracting textual content from each URL using a hybrid scraping approach comprising static HTTP extraction with fallback to headless browser-based dynamic rendering;
   (c) optimizing the extracted text using a large language model to produce structured, semantically rich content;
   (d) splitting the optimized text into overlapping chunks and generating vector embeddings for each chunk;
   (e) storing the embeddings with text metadata in a vector database;
   (f) generating an executive summary of the processed content using a large language model;
   (g) receiving a natural language query from a user;
   (h) embedding the query and retrieving the top-k most similar document chunks from the vector database;
   (i) generating a response grounded in the retrieved chunks using a large language model with conversation history context; and
   (j) presenting the response to the user through a web-based conversational interface.

**Claim 11.** The method of Claim 10, further comprising:
   (a) receiving a natural language visualization request from the user;
   (b) classifying the request intent as a visualization command;
   (c) retrieving relevant data from the vector database;
   (d) generating executable chart-rendering code through a large language model;
   (e) executing the code in a sandboxed environment; and
   (f) returning the rendered chart image to the user interface.

**Claim 12.** The method of Claim 10, further comprising:
   (a) receiving a natural language data export request from the user;
   (b) classifying the request intent as a data export command;
   (c) generating structured tabular data grounded in retrieved document content;
   (d) converting the structured data into a downloadable spreadsheet file; and
   (e) transmitting the file to the user interface for download.

**Claim 13.** The method of Claim 10, wherein step (b) comprises:
   (a) first attempting static content extraction using HTTP request libraries and content extraction libraries;
   (b) evaluating whether sufficient content was extracted based on a minimum character threshold; and
   (c) upon insufficient extraction, automatically invoking a headless browser to render the page with full JavaScript execution before content extraction.

**Claim 14.** The method of Claim 10, wherein the executive summary generation in step (f) is performed concurrently with the embedding and indexing steps (d) and (e), thereby reducing total processing time.

**Claim 15.** A non-transitory computer-readable storage medium storing instructions that, when executed by one or more processors, cause the one or more processors to perform operations comprising:
   (a) receiving a plurality of URLs from a user through a web interface;
   (b) extracting and combining textual content from the plurality of URLs using a hybrid static-dynamic web scraping pipeline;
   (c) optimizing the combined text for semantic search using a large language model;
   (d) generating vector embeddings for chunks of the optimized text and storing them in a cloud vector database;
   (e) generating an executive summary and presenting it to the user;
   (f) accepting natural language queries and generating context-grounded responses using retrieval-augmented generation;
   (g) generating data visualizations from natural language commands by producing and executing chart-rendering code; and
   (h) generating downloadable spreadsheet files from natural language data export requests.

---

### Inventors

- AJITH GEORGE SAM (22BD1A0581)
- ARCHITH SABBANI (22BD1A059G)
- SALONI SHARMA (22BD1A059H)
- RAHUL VALAVOJU (22BD1A059V)

### Institution

Keshav Memorial Institute of Technology (Autonomous), Narayanaguda, affiliated to JNTUH

### Academic Year

2025–2026

### Faculty Supervisor

Ms. Spoorthy H, Department of Computer Science and Engineering

---
