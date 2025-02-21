# Cloud-Based-Text-Summarizer

## Description 
Scalable cloud-based web application, which processes large PDF and text files, generating AI-powered summaries. The system uses Google Cloud Platform (GCP) with Terraform to automate infrastructure deployment and supports high traffic through serverless and managed services.

The app is built with Python (Fast API) for the backend and React for frontend.
The summarization service leverages Gemini to extract key points, making it ideal for scientists, researchers, and lawyers who need quick insights from extensive documents.

## Few Main features 
* Document Upload & Processing
* AI-Powered Summarization
* Scalable Real-Time Processing
* Two ways of explanation
* Authentication & Role-Based Access

## Typical Users
* Scientists
* Researches
* Lawyers 

## Roles of typical users
* Guest -	Can summarize a limited number of documents per day. No saved history.
* Registered User -	Stores history and supports file downloads.
* Premium User - Unlimited summarization.
* Admin -	Monitors system performance, API usage, billing and access control.

## Milestones
* 14.03 M1: Project Submission (brief description, few main features, roles of typical users)
* 04.04 M2: Project document (diagram, APIs design, Storage chars, Terraform, SLA, SLO, SLI)
* 04.04 M2: Presentation of the plan
* 30.05 M3: Final presentation + live demo

## Technologies
1. Backend – Python
2. Frontend - React
3. AI - Gemini
4. Cloud Functions – to process text
5. Google Cloud Storage – to store uploaded pdf files
6. Stored in GitHub (project + Terraform as modules)
7. Diagram - draw.io

## Versions
1. App that can take text and give back summary 
2. App that can take pdf and give back summary in pdf (Basic version)
3. App that you can use to browse the scientific files in internet and then get theirs summary
