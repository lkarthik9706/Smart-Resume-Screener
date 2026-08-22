# Smart Resume Screener

An AI-powered resume screening system that extracts structured information from PDF/DOCX resumes and intelligently matches candidates against a given job description.

The system uses Google's Gemini API for resume understanding and semantic job matching, while MongoDB stores structured candidate information and screening results.

---

## 1. Problem Statement

Recruiters often need to review a large number of resumes for a single job opening. Manual screening can be time-consuming and may depend heavily on keyword matching, which can miss candidates whose relevant skills are described differently.

Smart Resume Screener automates this initial screening process by extracting structured information from resumes and using an LLM to semantically compare candidate profiles with job descriptions.

The system produces an explainable match score, identifies matched and missing skills, highlights candidate strengths and weaknesses, and provides an AI-generated recruitment justification.

---

## 2. Objectives

The main objectives of the system are:

- Accept resumes in PDF and DOCX formats.
- Extract readable text from uploaded resumes.
- Convert unstructured resume content into structured candidate information.
- Extract skills, education, experience, projects, and certifications.
- Store structured resume data in MongoDB.
- Accept a job description from the recruiter.
- Compare the candidate profile with the job requirements using Gemini.
- Generate a match score from 1 to 10.
- Identify matched and missing skills.
- Provide strengths and weaknesses.
- Generate an explainable screening justification.
- Determine whether the candidate should be shortlisted.

---

## 3. Key Features

### Resume Upload

Supports:

- PDF
- DOCX

Maximum supported file size:

- 5 MB

### AI Resume Parsing

Gemini extracts structured information such as:

- Candidate name
- Email
- Phone
- Education
- Skills
- Experience
- Projects
- Certifications

### Semantic Job Matching

The system compares:

```
Candidate Resume
      +
Job Description
      ↓
Gemini
      ↓
Semantic Match Analysis
```
