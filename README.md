# Cloud-Based-Text-Summarizer

## Description 
Scalable cloud-based web application, which processes large PDF and text files, generating AI-powered summaries. The system uses Google Cloud Platform (GCP) with Terraform to automate infrastructure deployment and supports high traffic through serverless and managed services.

The app is built with Python (Fast API) for the backend and React for frontend.
The summarization service leverages Gemini to extract key points, making it ideal for scientists, researchers, and lawyers who need quick insights from extensive documents.

## Few Main features 
* Document Upload & Processing
* AI-Powered Summarization
* Scalable Real-Time Processing
* Tree ways of explanation (Scientific, Regular, Simple)
* Tree formats (Short, Long, Bullet Points)
* Authentication & Role-Based Access

## Typical Users
* Scientists
* Researches
* Lawyers
* Students

## Roles of typical users
* Registered User -	Can summarize a limited number of documents per day.
* Premium User - More summarizations.
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
4. DB - PostgreSQL (Google Cloud SQL)
5. Google Cloud Storage – to store summary files
6. Stored in GitHub (as submodules - backend + frontend + Terraform)
7. Diagram - draw.io

---

# API design 

## API Overview
- **Base URL for backend:** `https://cbts-backend-854061077838.europe-central2.run.app`
- **Base URL for frontend:** `https://cbts-frontend.vercel.app`
- **Authentication:** Bearer Token 
- **Rate Limiting:** Based on user role (Registered, Premium, Enterprise)
- **Response Format:** JSON (`application/json`)
- **Status Codes:**  
  - `200 OK` → Success  
  - `400 Bad Request` → Invalid Request  
  - `401 Unauthorized` → Authentication Required  
  - `403 Forbidden` → Insufficient Permission
  - `422 Validation error` → Insufficient Entity  
  - `500 Internal Server Error` → Unexpected Error  

---

## API Endpoints
### Process Summarization
- **Endpoint:** `POST /summary/summarize`
- **Description:** Starts the summarization process for an uploaded file.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  ```
- **Response:**
  ```json
  {
    "summary": "This is a summarized version of the document...",
    "gcs_path": "/summary"
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
- **Response:**
  ```json
  {
    "summary": "This is a summarized version of the document..."
  }
  ```

---

### Download summary
- **Endpoint:** `GET /summary/{file_id}/download`
- **Description:** Allows users to download the summary.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  ```
- **Response:**
  ```
  Content-Disposition: attachment; filename="summary.txt"
  Content-Type: text/plain
  ```

---

### Get User Summarization History
- **Endpoint:** `GET /history`
- **Description:** Returns a list of processed summaries for a user.
- **Headers:**
  ```http
  Authorization: Bearer {access_token}
  ```
- **Response:**
  ```json
    [
  {
    "id": 1,
    "filename_hash": "jd2d1jd",
    "user_id": 1,
    "filename": "summary.pdf"
  }
  ]
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
    "email": "user@example.com",
    "username": "user@example.com",
  }
  ```

- **Endpoint:** `POST /auth/login`
- **Description:** User authentication.
- **Request:**
  ```json
  {
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

# Security Measures
OAuth2 Authentication with Bearer token for API access.

## Rate Limits
| Plan | Max Number of Summarizations | Max File Size |
|------|---------------------|--------------|
| Registered | 5 | 5MB |
| Premium | 50 | 50MB |
| Enterprise | 200 | 500MB |

---

# Storage Characteristics 
## Google Cloud Storage
- Unstructured (stores summary files)
- NoSQL (Object storage, not relational)
- Strong Consistency (for newly written objects)
- Eventual Consistency (for object listing in large-scale cases)
- Highly Scalable (Petabytes+)
- Read & Write (Supports read, write, download and delete operations)

## Google Cloud SQL (PostgreSQL DB)
- Structured (Relational database with tables, rows, and columns)  
- SQL (Uses structured query language for querying and managing data)
- Strong Consistency (Ensures immediate visibility of committed transactions) 
- Scalable (Supports from small databases to terabytes of data, depending on instance size) 
- Read & Write (Supports both read and write operations, with role-based access control)

## DB diagram 
<img width="646" alt="db diagram" src="https://github.com/user-attachments/assets/8349a74c-dd8e-432e-8429-d4d6bb13c0f4" />

# Diagram with services and their connections
# Terraform 
# SLA
# SLO
# SLI



