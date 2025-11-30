# Architecture

## Overview

The Recruitment Screening AI uses document AI and NLP to extract candidate information, match against criteria, and generate scored shortlists.

## Components

### Document Parser
- **Technology:** Azure Form Recognizer / AWS Textract
- **Purpose:** Extract text and structure from CVs and application forms
- **Formats:** PDF, DOCX, images

### Entity Extractor
- **Technology:** Azure OpenAI / spaCy NER
- **Extracts:** Skills, qualifications, experience, dates, employers
- **Output:** Structured candidate profile

### Criteria Matcher
- **Technology:** Semantic similarity + rule-based matching
- **Function:** Compare candidate profile against job criteria
- **Output:** Score per criterion with evidence

### Bias Detector
- **Technology:** Fairness ML models
- **Function:** Identify potential bias in shortlisting patterns
- **Alerts:** Flag concerning patterns for review

### ATS Integration
- **Connectors:** Tribepad, Jobtrain, Networx
- **Data flow:** Pull applications, push scores/recommendations
- **Auth:** OAuth 2.0

## Data Flow

```
Applications → Document Parser → Entity Extractor
                                       ↓
                              Candidate Profile
                                       ↓
Job Criteria → Criteria Matcher → Scored Results
                                       ↓
                              Bias Detection
                                       ↓
                              Ranked Shortlist → ATS
```

## Security

- All candidate data encrypted (AES-256)
- UK data residency only
- Role-based access control
- Full audit logging
- 6-month data retention (configurable)
