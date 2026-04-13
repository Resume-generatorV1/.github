# Agentic AI Resume & Cover Letter Generator

I developed an intelligent resume and cover letter generation system that leverages LLMs to dynamically tailor application materials based on a user's profile and a given job description. The system is designed to go beyond simple text generation by incorporating structured user data, skill extraction, and selective content rewriting to produce highly relevant and ATS-optimized outputs.

The application allows users to provide a job link or job description, which is then analyzed to extract key skills and requirements. Using this information, the system intelligently selects and refines relevant content from the user's profile to generate a customized resume and cover letter.

The frontend was built using **Next.js**, while the backend was implemented using **Python (FastAPI)** with **LangChain** and **DeepSeek LLM** for orchestration and generation. A **PostgreSQL** database is used to persist user data and intermediate processing results.

**NOTE: All repositories except skill_extractor are private.**

---

## System Design and Workflow

The system follows a structured yet flexible pipeline combining deterministic processing with LLM-based refinement:

- Users upload their resume (in LaTeX format), which is parsed to extract structured information such as education, experience, projects, and skills.
- This information is stored in a PostgreSQL database, enabling reuse and eliminating repeated parsing or prompting.
- Users can additionally manage and toggle projects (active/inactive), allowing fine-grained control over what appears in generated resumes.
- When a job description or link is provided, the system extracts and ranks relevant skills, then compares them against the user's stored profile.
- Based on this comparison, the system selects the most relevant projects and dynamically rewrites only specific sections of the resume instead of regenerating the entire document.

This selective editing approach significantly reduces LLM usage, improving both performance and cost efficiency.

---

## Key Features and Technical Highlights

### 1. Job Description Extraction

- Built a robust **URL extraction pipeline** supporting major job platforms such as Workday, Lever, and Greenhouse.
- Used **BeautifulSoup** for static pages and **Playwright** as a fallback for dynamically rendered job postings.
- Ensured high coverage across diverse job posting formats.

---

### 2. Custom Skill Extraction Engine

- Developed a **fully local, modular skill extraction system** without relying on LLMs or external APIs, built on **spaCy (v3.x)**.
- Multi-layered taxonomy combining the **ESCO dataset** (14,000+ skills), **Stack Overflow tags** (~5,000 technologies), and **custom curated skills** (e.g., Snowflake, BigQuery).
- Extracted skills are cached using the job URL as a primary key or **SHA-256 hashing** for raw job descriptions, avoiding recomputation for repeated queries.

---

### 3. Intelligent Resume Generation

- Compares extracted job skills with the user's existing resume content.
- Dynamically selects the **most relevant projects** from the database.
- Uses **LangChain + DeepSeek LLM** to:
  - Rewrite project descriptions for better alignment
  - Enhance skill sections (e.g., inferring related technologies like PostgreSQL from SQL)
- Performs **targeted LaTeX replacement**, modifying only necessary sections while preserving formatting and structure.
- Implements safeguards to prevent **hallucination or skill exaggeration**, ensuring factual consistency.

---

### 4. Cover Letter Generation

- Generates personalized cover letters using the user's complete profile including education, experience, projects, and skills.
- Aligns narrative with job requirements for stronger personalization and coherence.

---

### 5. Data Persistence and Optimization

- Stores user profile data, extracted skills, and cached job descriptions in PostgreSQL.
- Reduces redundant computation and LLM calls, improving both **latency and cost efficiency**.

---

## System Architecture

| Layer | Technology |
|---|---|
| Frontend | Next.js |
| Backend | FastAPI (Python) |
| LLM Orchestration | LangChain + DeepSeek |
| Database | PostgreSQL |
| Parsing | Custom LaTeX parser |
| Scraping | BeautifulSoup + Playwright |
| NLP | spaCy-based skill extraction engine |

---

## Learning and Outcome

This project helped me gain hands-on experience in building end-to-end AI-powered systems that combine traditional software engineering with modern LLM capabilities. I explored efficient ways to integrate LLMs into production systems by minimizing unnecessary calls and using structured data wherever possible.

I also developed a deeper understanding of:

- Designing hybrid pipelines (rule-based + LLM)
- Preventing hallucination in generated content
- Optimizing systems for cost and performance
- Building scalable backend architectures with persistent state
