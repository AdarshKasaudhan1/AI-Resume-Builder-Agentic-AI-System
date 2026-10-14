# AI Resume Builder — Agentic AI System

An AI-powered resume optimization tool that analyzes a candidate's resume against a target job description, identifies skill gaps, recommends improvements, and generates a tailored, ATS-friendly resume.

Built using Python, Streamlit, LangChain, LangGraph, and Groq's Llama 3.3 model, the application uses a four-agent workflow to break resume optimization into specialized tasks.

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [How It Works](#how-it-works)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Example Usage](#example-usage)
- [Troubleshooting](#troubleshooting)
- [Limitations](#limitations)

## Overview

Creating a resume for every job application can be time-consuming. Candidates need to understand job requirements, identify relevant skills, and present their experience in a format that applicant tracking systems (ATS) can process.

The AI Resume Builder streamlines this process through a multi-agent architecture. Each agent performs a specific task, from interpreting job descriptions to generating tailored resume content.

The application provides an interactive Streamlit interface for submitting resume information and reviewing AI-generated recommendations.

## Key Features

- **Resume Parsing:** Extract resume content from PDF and DOCX files.
- **Job Description Analysis:** Analyze job requirements from text or supported URLs.
- **Resume Match Scoring:** Generate an AI-based assessment of resume alignment with a target role.
- **Skill Gap Analysis:** Identify relevant skills and qualifications that may be missing from the resume.
- **Project Recommendations:** Suggest relevant project improvements based on the target job description.
- **ATS-Friendly Resume Generation:** Generate tailored resume content aligned with the job requirements.
- **Multi-Agent Processing:** Divide the workflow into four specialized agents.
- **Interactive Interface:** Use the application through a Streamlit web interface.

> AI-generated scores and recommendations are advisory assessments, not guarantees of ATS performance or interview shortlisting.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application logic and workflow implementation |
| Streamlit | Interactive web interface |
| LangGraph | Multi-agent workflow orchestration |
| LangChain | Language model integration and application components |
| Groq — Llama 3.3 | Language model inference |
| PDFPlumber | PDF text extraction |
| Python-Docx | DOCX document processing |
| Firecrawl | Web content extraction where supported |
| BeautifulSoup | HTML parsing |
| HTTPX | HTTP requests and API communication |

Dependencies are listed in `requirements.txt`.

## How It Works

The application uses four specialized agents coordinated through a multi-agent workflow.

### Agent 1: Job Description Parser

**Purpose:** Understand the target role.

- Processes the job description.
- Extracts relevant skills, qualifications, and responsibilities.
- Structures the information for downstream analysis.

**Output:** A structured representation of the job requirements.

### Agent 2: Resume Evaluator

**Purpose:** Assess the candidate's resume against the target role.

- Reviews the resume content.
- Evaluates its relevance to the job description.
- Identifies areas of alignment and potential improvement.

**Output:** A resume evaluation and match assessment.

### Agent 3: Gap Analyst & Project Recommender

**Purpose:** Identify improvement opportunities.

- Compares candidate skills with job requirements.
- Highlights potential skill gaps.
- Recommends relevant project ideas or improvements.

**Output:** A list of improvement areas and tailored project recommendations.

### Agent 4: Resume Writer

**Purpose:** Generate tailored resume content.

- Uses the preceding analysis to guide resume rewriting.
- Emphasizes relevant skills and experience.
- Produces structured content aligned with the target role.

**Output:** An AI-generated, job-specific resume draft.

### Workflow Summary

```text
Resume + Job Description
          |
          v
   Job Description Parser
          |
          v
     Resume Evaluator
          |
          v
 Gap Analyst & Project Recommender
          |
          v
       Resume Writer
          |
          v
 Tailored Resume and Recommendations
```

The agents divide the overall task into manageable stages, helping organize the analysis and content-generation process.

## Prerequisites

Before installing the application, ensure you have:

- Python installed on your system.
- Git installed for cloning the repository.
- A Groq API key for model access.
- A Firecrawl API key if the URL-based extraction functionality requires it.
- An internet connection for API access and dependency installation.

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/AdarshKasaudhan1/AI-Resume-Builder-Agentic-AI-System.git
```

### 2. Navigate to the project directory

```bash
cd AI-Resume-Builder-Agentic-AI-System
```

### 3. Create a virtual environment

```bash
python -m venv .venv
```

Activate the environment.

**Windows — Command Prompt:**

```bat
.venv\Scripts\activate
```

**Windows — PowerShell:**

```powershell
.\.venv\Scripts\Activate.ps1
```

**macOS or Linux:**

```bash
source .venv/bin/activate
```

### 4. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

This installs the Python packages specified by the project.

## Configuration

### 1. Create the environment file

Copy `.env.example` to a new file named `.env` in the project root.

**Windows — Command Prompt:**

```bat
copy .env.example .env
```

**PowerShell:**

```powershell
Copy-Item .env.example .env
```

**macOS or Linux:**

```bash
cp .env.example .env
```

### 2. Add your API keys

Open `.env` and replace the placeholder values with your own credentials.

```dotenv
GROQ_API_KEY=your_groq_api_key
FIRECRAWL_API_KEY=your_firecrawl_api_key
```

Obtain API keys from the relevant service providers.

**Security note:** Never commit your `.env` file or expose API keys in source code, screenshots, or public repositories.

## Running the Application

From the project root, activate your virtual environment and run:

```bash
streamlit run app.py
```

Streamlit will display a local URL in the terminal. Open that URL in your browser to access the application.

If your local project configuration uses a different entry-point file, check the repository's application instructions before running it.

## Example Usage

The following is an illustrative example of how a candidate might use the application.

### Input

**Target role:** Technical Writer Intern

**Job description:**

```text
We are looking for a technical writer who can
create clear product documentation, understand
REST APIs, work with Git, and use AI tools to
draft and review technical content.
```

**Resume information:**

```text
Skills: Python, REST APIs, Git, SQL

Project: AI Resume Builder

Technologies: Streamlit, LangGraph, LangChain

Experience: Built an AI-powered application
that analyzes resumes and job descriptions.
```

### Expected types of output

Depending on the implemented workflow, the application can provide:

- **Match assessment:** An AI-generated evaluation of the resume's relevance to the target role.
- **Skill gap analysis:** Potential gaps, such as limited demonstrated experience with Markdown documentation.
- **Project recommendations:** Suggestions for documenting the AI Resume Builder with a detailed README.
- **Tailored resume draft:** Revised content emphasizing relevant technical knowledge and project experience.

These examples illustrate the intended usage; they are not guaranteed outputs or measured results from a live application run.

## Troubleshooting

| Problem | Possible cause | Suggested resolution |
|---|---|---|
| `ModuleNotFoundError` | Dependencies are missing or the wrong environment is active. | Activate the virtual environment and run `pip install -r requirements.txt`. |
| API authentication error | An API key is missing, invalid, or incorrectly configured. | Check the `.env` file and verify the relevant API credentials. |
| Rate-limit error | The API provider has reached its request limit. | Check the provider's usage limits and retry when permitted. |
| Resume parsing fails | The document is unreadable, malformed, or unsupported. | Try a valid PDF or DOCX file and verify that it contains readable text. |
| URL extraction fails | The URL is inaccessible or extraction credentials are unavailable. | Check the URL, connectivity, and Firecrawl configuration where applicable. |
| Streamlit command not found | Streamlit is not installed in the active environment. | Activate the virtual environment and reinstall the project dependencies. |
| Application fails during execution | A configuration issue or unexpected exception occurred. | Review the terminal traceback, check configuration values, and inspect the relevant application logs. |

## Limitations

- AI-generated assessments may be inaccurate or incomplete.
- Match scores should be treated as estimates rather than official ATS scores.
- Resume recommendations depend on the quality of the input resume and job description.
- URL-based job description extraction may depend on website accessibility and third-party service availability.
- Generated resume content should be reviewed for factual accuracy before use.

## Contributing

Contributions and suggestions are welcome.

1. Fork the repository.
2. Create a branch for your changes.
3. Make and test your updates.
4. Submit a pull request describing the changes.

## License

Check the repository for an applicable license before redistributing or reusing this project.

## Author

**Adarsh Kasaudhan**

- GitHub: [AdarshKasaudhan1](https://github.com/AdarshKasaudhan1)
- Project Repository: [AI Resume Builder — Agentic AI System](https://github.com/AdarshKasaudhan1/AI-Resume-Builder-Agentic-AI-System)
