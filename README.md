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
* Enterprise User - Highload summarization with prioritization.
* Admin -	Monitors system performance, API usage, billing and access control.

## Milestones
* 14.03 M1: Project Submission (brief description, few main features, roles of typical users)
* 04.04 M2: Project document (diagram, APIs design, Storage chars, Terraform, SLA, SLO, SLI)
* 04.04 M2: Presentation of the plan
* 30.05 M3: Final presentation + live demo

## Technologies
1. Backend – Python - Google Cloud
2. Frontend - React - Vercel
3. AI - Gemini
4. DB - PostgreSQL
5. Google Cloud Storage – to store pdf files
6. Stored in GitHub (as submodules - backend + frontend + Terraform)
7. Diagram - draw.io

## Versions
1. App that can take pdf and give back summary (Demo version)
2. App, where user can upload pdf file, summarize it, check summary status, download summary and check history
3. App, where user can browse scientific files in internet and then get theirs summary

---

# API design 

## API Overview
- **Base URL for backend:** `https://cbts-backend-854061077838.europe-central2.run.app`
- **Base URL for frontend:** ``
- **Authentication:** Bearer Token 
- **Rate Limiting:** Based on user role (Guest/Registered, Premium, Enterprise)
- **Response Format:** JSON (`application/json`)
- **Status Codes:**  
  - `200 OK` → Success  
  - `400 Bad Request` → Invalid Request  
  - `401 Unauthorized` → Authentication Required  
  - `403 Forbidden` → Insufficient Permission  
  - `500 Internal Server Error` → Unexpected Error  

---

## API Endpoints
### Upload Document
- **Endpoint:** `POST /upload`
- **Description:** Allows users to upload documents for summarization.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  Content-Type: multipart/form-data
  ```
- **Request:**
  ```multipart/form-data
  file: {PDF/TXT file}
  ```
- **Response:**
  ```json
  {
    "file_id": "abc123",
    "status": "processing",
    "message": "File uploaded successfully"
  }
  ```

---

### Process Summarization
- **Endpoint:** `POST /summarize/{file_id}`
- **Description:** Starts the summarization process for an uploaded file.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  ```
- **Response:**
  ```json
  {
    "file_id": "abc123",
    "status": "processing"
  }
  ```

---

### Get Summary
- **Endpoint:** `GET /summary/{file_id}`
- **Description:** Retrieves the generated summary for a processed document.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  ```
- **Response (If Ready):**
  ```json
  {
    "file_id": "abc123",
    "status": "completed",
    "summary": "This is a summarized version of the document..."
  }
  ```
- **Response (If Still Processing):**
  ```json
  {
    "file_id": "abc123",
    "status": "processing",
    "message": "Your summary is still being processed."
  }
  ```

---

### Download as PDF, TXT, or DOCX
- **Endpoint:** `GET /summary/{file_id}/download`
- **Description:** Allows users to download the summary in different formats.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  ```
- **Query Params:**
  ```
  format = "pdf" | "txt" | "docx"
  ```
- **Response:**
  ```
  Content-Disposition: attachment; filename="summary.pdf"
  Content-Type: application/pdf
  ```

---

### Get User Summarization History
- **Endpoint:** `GET /user/history`
- **Description:** Returns a list of processed summaries for a user.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  ```
- **Response:**
  ```json
  {
    "user_id": "user_789",
    "history": [
      {
        "file_id": "abc123",
        "filename": "report.pdf",
        "date": "2025-02-21",
        "status": "completed"
      },
      {
        "file_id": "xyz456",
        "filename": "thesis.txt",
        "date": "2025-02-18",
        "status": "failed"
      }
    ]
  }
  ```

---

### Authentication
- **Endpoint:** `POST /auth/registration`
- **Description:** User registration.
- **Request:**
  ```json
  {
    "email": "user@example.com",
    "username": "user@example.com",
    "password": "securepassword"
  }
  ```
- **Response:**
  ```json
  {
    "access_token": "eyJhbGciOiJIUzI1..."
  }
  ```

- **Endpoint:** `POST /auth/login`
- **Description:** User authentication.
- **Request:**
  ```json
  {
    "email": "user@example.com",
    "password": "securepassword"
  }
  ```
- **Response:**
  ```json
  {
    "access_token": "eyJhbGciOiJIUzI1..."
  }
  ```

### Refresh Token
- **Endpoint:** `POST /auth/refresh`
- **Description:** Refreshes the user's access token.
- **Response:**
  ```json
  {
    "access_token": "new_access_token"
  }
  ```

---

### Admin API - Get System Analytics
- **Endpoint:** `GET /admin/analytics`
- **Description:** Provides insights on system performance & user activity.
- **Headers:**
  ```http
  Authorization: Bearer {admin_token}
  ```
- **Response:**
  ```json
  {
    "total_summaries": 12500,
    "active_users": 3500
  }
  ```


## Rate Limits
| Plan | Max Number of Summarizations | Max File Size |
|------|---------------------|--------------|
| Guest/Registered | 5 | 5MB |
| Premium | 50 | 50MB |
| Enterprise | 200 | 500MB |

---

## Security Measures
- **OAuth2 / Firebase Authentication** for API access.

