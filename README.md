# LearnPilot AI 🎓

### AI-Powered Personalized Learning and Lecture Recommendation System

LearnPilot AI is a full-stack educational web application that helps students organize their studies, understand academic concepts using AI, and discover relevant educational video lectures. It combines a personalized learning dashboard, an AI study assistant, syllabus management, notes, quizzes, and study planning in one platform.

---

## 📌 Table of Contents

- [About the Project](#-about-the-project)
- [Objectives](#-objectives)
- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [System Architecture](#-system-architecture)
- [Prerequisites](#-prerequisites)
- [Installation and Setup](#-installation-and-setup)
- [API Configuration](#-api-configuration)
- [Testing](#-testing)
- [API Endpoints](#-api-endpoints)
- [Security and Privacy](#-security-and-privacy)
- [Limitations](#-limitations)
- [Future Enhancements](#-future-enhancements)
- [Author](#-author)

---

## 📖 About the Project

Students often use multiple platforms to find lecture videos, understand difficult concepts, prepare notes, practice quizzes, and manage their study schedules.

LearnPilot AI aims to simplify this process by bringing these learning activities together in a single web application.

The application uses Google Gemini for AI-powered study assistance and the YouTube Data API to retrieve real educational video results. Students can manage their curriculum, upload text-based syllabus PDFs, create notes and quizzes, bookmark lectures, and track their learning progress.

The application uses a guest-profile approach. Learning data is stored in an SQLite database and associated with a randomly generated browser profile ID. This is designed for convenient demonstration and personal use, not secure account authentication.

## 🎯 Objectives

- Provide students with a centralized learning platform.
- Generate AI-assisted explanations for academic questions.
- Recommend relevant educational lectures based on searched topics.
- Simplify syllabus organization and topic tracking.
- Support revision through notes and multiple-choice quizzes.
- Help students plan study sessions and monitor their progress.
- Demonstrate the integration of frontend, backend, database, and external APIs in a full-stack application.

## ✨ Features

### 1. Personalized Dashboard
- View learning statistics and progress.
- Access curriculum, notes, quizzes, tasks, and recommendations.
- Organize learning activities from a single interface.

### 2. Curriculum Management
- Add, rename, and delete subjects and topics.
- Track topic completion and learning status.
- Upload text-based syllabus PDFs.
- Review suggested topic lines before adding them to the curriculum.

### 3. AI Study Assistant
- Ask academic questions and receive AI-generated explanations.
- Use recent conversation history as context.
- Get help understanding technical concepts.
- Powered by the configured Gemini or supported OpenAI-compatible provider.

### 4. Lecture Recommendation System
- Search for educational videos using the YouTube Data API v3.
- Retrieve actual video IDs, titles, channel names, thumbnails, durations, and view counts when available.
- Rank results using keyword-based relevance scoring.
- Filter results by available metadata and matching channel or title labels.
- Open the original YouTube videos.
- Bookmark lectures and mark them as completed.

### 5. AI Notes Generator
- Generate study notes using the configured AI provider.
- Edit, save, and delete notes.
- Organize learning material for revision.

### 6. AI Quiz Generator
- Generate multiple-choice questions.
- Submit answers and view quiz results.
- Store scores for later review.

### 7. Study Planner
- Create and edit study tasks.
- Mark tasks as completed.
- Delete tasks that are no longer needed.

### 8. Profile and Progress Tracking
- Save profile preferences.
- View dashboard statistics derived from stored learning records.
- Maintain separate learning data for different browser profile IDs.

### 9. Backend Validation and API Documentation
- Validate incoming API requests.
- Apply Cross-Origin Resource Sharing (CORS) configuration.
- Provide a health endpoint for checking service configuration.
- Expose interactive API documentation through FastAPI.

---

## 🛠️ Technology Stack

| Component | Technology |
|---|---|
| Frontend | React |
| Frontend tooling | Vite |
| Programming languages | JavaScript, Python |
| Backend framework | FastAPI |
| Database | SQLite |
| Database access | SQLAlchemy |
| AI integration | Google Gemini API |
| Alternative AI integration | Supported OpenAI-compatible API |
| Lecture search | YouTube Data API v3 |
| PDF text extraction | pypdf |
| API testing | pytest |
| Development tools | Visual Studio Code, Git, GitHub |

---

## 🏗️ System Architecture

LearnPilot AI follows a client-server architecture. The frontend communicates with the backend through HTTP API requests, while the backend manages database operations and integrations with external services.

```text
             STUDENT
                |
                v
       React + Vite Frontend
                |
          HTTP API Requests
       (Fetch API + Profile ID)
                |
                v
          FastAPI Backend
                |
       Request Validation
                |
       +--------+---------+----------------+
       |        |         |                |
       v        v         v                v
    SQLite   Gemini    YouTube API       pypdf
    Database   API      Integration    PDF Text
       |        |         |            Extraction
       +--------+---------+----------------+
                |
                v
       Responses to Frontend
                |
                v
       Dashboard and Learning UI
```

### Architecture Explanation

1. **Frontend:** React and Vite provide the user interface for managing learning activities.
2. **API communication:** The frontend sends HTTP requests to the FastAPI backend and includes a browser profile ID to associate requests with the relevant learning data.
3. **Backend:** FastAPI handles requests, validates input, and coordinates application logic.
4. **Database:** SQLite stores curriculum, notes, tasks, quiz results, profile preferences, and lecture-related state.
5. **AI integration:** Gemini generates responses, notes, and quizzes when correctly configured.
6. **Lecture search:** YouTube Data API v3 supplies video search results and metadata.
7. **PDF processing:** pypdf extracts selectable text from supported syllabus PDFs.

---

## 💻 Prerequisites

Install the following software before running the application:

| Requirement | Purpose |
|---|---|
| Python 3.10 or later | Runs the backend |
| Node.js 18 or later | Runs the frontend tooling |
| npm | Installs frontend dependencies |
| Git | Version control |
| Gemini API key | AI assistant, notes, and quiz generation |
| YouTube Data API key | Live YouTube lecture search |

API availability, model access, and usage quotas depend on the provider and your account.

---

## 🚀 Installation and Setup

### Step 1: Clone the Repository

Open a terminal and run:

```bash
git clone https://github.com/Safi-dev/LearnPilotAI.git
cd LearnPilotAI
```

Alternatively, download the repository as a ZIP file from GitHub and extract it.

### Step 2: Set Up the Backend

Open a terminal in the project root:

```powershell
cd backend
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

If PowerShell blocks virtual environment activation, run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

### Step 3: Configure Environment Variables

If the project includes `backend/.env.example`, create your local environment file:

```powershell
Copy-Item .env.example .env
notepad .env
```

Run these commands from inside the `backend` directory.

Add your actual API keys and the configuration variables expected by your backend. For example:

```dotenv
DATABASE_URL=sqlite:///./learnpilot.db
FRONTEND_ORIGINS=http://localhost:5173,http://127.0.0.1:5173

LLM_PROVIDER=gemini
GEMINI_API_KEY=YOUR_GEMINI_API_KEY
LLM_MODEL=YOUR_SUPPORTED_GEMINI_MODEL
DEMO_MODE=false

YOUTUBE_API_KEY=YOUR_YOUTUBE_API_KEY
```

Replace the placeholders with your actual configuration values. Use a Gemini model supported by your Google AI Studio project and the application's integration.

**Important:** Never commit the real `.env` file to GitHub.

### Step 4: Start the Backend

From the `backend` directory, with the virtual environment activated:

```powershell
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

The backend should be available at:

- API base: `http://127.0.0.1:8000/api`
- Health check: `http://127.0.0.1:8000/api/health`
- Interactive API documentation: `http://127.0.0.1:8000/docs`

Keep this terminal open.

### Step 5: Start the Frontend

Open a second terminal in the main project directory, where `package.json` is located.

Run:

```powershell
npm install
npm run dev
```

Open the local URL displayed by Vite, usually:

`http://localhost:5173`

Keep both the frontend and backend running during development.

### Step 6: Verify the Configuration

Open:

`http://127.0.0.1:8000/api/health`

Confirm that the backend is running and that the AI and YouTube integrations are configured successfully.

If the health endpoint reports missing or invalid configuration, review the relevant environment variables and provider settings. Never share your actual API keys when requesting help.

---

## 🧪 Testing

The backend includes a pytest-based test suite, if present in the repository.

From the `backend` directory, with the virtual environment activated, run:

```powershell
pytest tests/ -v
```

Tests may cover:

- Backend health and configuration validation.
- AI and YouTube integration error handling.
- Mocked external API responses.
- Profile and curriculum operations.
- Dashboard and other API functionality.

External API tests should use mocks where appropriate so that ordinary test runs do not require live API calls or consume API quota.

---

## 🔌 API Endpoints

The backend exposes REST-style endpoints for frontend operations. The following is a feature-oriented overview; consult the running API documentation for the exact routes and request formats implemented in the current version.

| Endpoint or group | Purpose |
|---|---|
| `/api/health` | Check backend and integration configuration |
| `/api/profile` | Read or update profile preferences |
| `/api/curriculum/subjects` | Manage subjects |
| `/api/curriculum/subjects/{id}/topics` | Add topics to a subject |
| `/api/curriculum/topics/{id}` | Update or delete topics |
| `/api/curriculum/upload` | Upload and process syllabus text |
| `/api/lectures/search` | Search for lecture videos |
| `/api/lectures/saved` | Retrieve saved lecture information |
| `/api/bookmarks` | Manage lecture bookmarks |
| `/api/assistant/chat` | Submit an AI chat message |
| `/api/assistant/history` | Access conversation history |
| `/api/notes` | Manage study notes |
| `/api/notes/generate` | Generate AI-assisted notes |
| `/api/quizzes/generate` | Generate quizzes |
| `/api/quizzes/submit` | Submit quiz answers |
| `/api/quizzes/results` | Retrieve quiz results |
| `/api/tasks` | Manage study tasks |
| `/api/dashboard` | Retrieve dashboard statistics |
| `/api/progress` | Retrieve learning progress |

Open `http://127.0.0.1:8000/docs` while the backend is running to inspect the actual API routes, parameters, and response schemas.

---

## 🔐 Security and Privacy

LearnPilot AI is a student mini-project and should not be treated as a production-ready authentication system.

- API keys must remain in backend environment variables.
- Never commit real `.env` files or API secrets to GitHub.
- Keep the repository private if you do not want your source code publicly accessible.
- The guest profile ID is a convenience mechanism, not proof of identity.
- Browser profile IDs do not replace authentication, authorization, or secure access controls.
- Do not store sensitive personal information in a demonstration deployment.
- Configure CORS for the frontend origins you actually use.
- Review provider usage limits and security requirements before deploying the application.

---

## ⚠️ Limitations

- The application requires internet access for live Gemini and YouTube API features.
- External API usage is subject to provider availability, quotas, and rate limits.
- Guest profiles are not secure user accounts and do not provide password-based authentication.
- Syllabus extraction handles selectable PDF text; scanned or image-only PDFs require OCR, which is not included by default.
- Lecture relevance ranking uses keyword-overlap heuristics rather than a trained recommendation model.
- Platform filters based on channel or title labels do not independently search other educational platforms.
- SQLite is suitable for local development and demonstrations, but a larger multi-user deployment may require a production database and additional infrastructure.
- Production deployment requires appropriate authentication, secret management, monitoring, and security hardening.

---

## 🔮 Future Enhancements

- Implement secure registration, login, and session management.
- Introduce more advanced recommendations using student preferences and learning history.
- Add OCR support for scanned syllabus documents.
- Include learning analytics and visual progress reports.
- Add reminders and calendar integration for study planning.
- Improve accessibility and mobile responsiveness.
- Add automated deployment and continuous integration.
- Support additional educational content providers.
- Improve production security, database scalability, and error monitoring.

---

## 🎓 Applications

- College and university study assistance.
- Syllabus organization and topic tracking.
- Finding supplementary educational lectures.
- Preparing revision notes and practice quizzes.
- Planning study sessions and monitoring progress.
- Demonstrating full-stack development and third-party API integration.

---

## 👨‍💻 Author

**Safi-dev**

GitHub: [https://github.com/Safi-dev](https://github.com/Safi-dev)

Project repository: [LearnPilot AI](https://github.com/Safi-dev/LearnPilotAI)

---

## 📄 License

No license has been specified for this repository yet. Unless a license is added, reuse and redistribution are subject to applicable copyright law and the repository owner's permissions.

---

**LearnPilot AI — Making personalized learning more organized, accessible, and engaging.**
