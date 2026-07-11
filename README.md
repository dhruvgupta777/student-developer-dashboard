<div align="center">

# 🎓 StudentOS

### Your complete student developer dashboard

*Track GPA · Monitor coding profiles · Manage job applications · Solve assignments with AI*

![StudentOS Dashboard](https://img.shields.io/badge/Status-Live-brightgreen)
![Java](https://img.shields.io/badge/Java-17-orange)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5-green)
![React](https://img.shields.io/badge/React-19-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17-blue)

</div>

---

## 📌 What is StudentOS?

As a B.tech CSE student, you're constantly switching between tabs — checking your GPA on one site, tracking job applications on a spreadsheet, checking Codeforces rating on another tab, asking ChatGPT for assignment help somewhere else.

**StudentOS fixes that.**

It's a unified dashboard that brings everything a CS student needs into one clean, fast interface. Built entirely from scratch with a production-grade Spring Boot backend and a React frontend.

---

## ✨ Features

### 📊 GPA Tracker
- Add semester SGPAs and track academic performance over time
- Beautiful donut charts for each semester
- Bar graph showing performance trend across all semesters
- Built-in CGPA calculator using weighted formula: `CGPA = Σ(SGPA × Credits) ÷ Σ(Credits)`

### 💼 Job Application Tracker
- Add company applications with role and notes
- Update status: Applied → Interview → Offer → Rejected
- Stats overview showing total applications at each stage
- Delete applications you no longer want to track

### ⌨️ Coding Profiles
- Connect GitHub username → see repos, followers, avatar
- Connect LeetCode username → see global ranking and stats
- Connect Codeforces handle → see rating, max rating, rank with avatar

### 🧩 Problem Practice
- Browse 200+ Codeforces problems directly inside the app
- Filter by rating (800 to 2000+) and topic tags
- Search problems by name
- Click any problem to open it directly on Codeforces

### 🤖 AI Assignment Solver
- Floating chatbot in bottom right corner
- WhatsApp-style chat interface
- Ask any academic question — math, DSA, theory, code
- Powered by Llama 3.3 70B via Groq API (free)

### 🔐 Secure Authentication
- JWT-based authentication
- BCrypt password hashing
- Protected API routes — each user only sees their own data

---

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|-----------|---------|
| Java 17 | Core language |
| Spring Boot 3.5 | Backend framework |
| Spring Security | Authentication & authorization |
| JWT (jjwt 0.11.5) | Stateless token auth |
| Spring Data JPA | Database ORM |
| Hibernate | SQL generation |
| PostgreSQL 17 | Primary database |
| Maven | Build tool |

### Frontend
| Technology | Purpose |
|-----------|---------|
| React 19 | UI framework |
| Vite | Build tool |
| Tailwind CSS | Styling |
| Axios | HTTP client |

### External APIs
| API | Used for |
|-----|---------|
| GitHub REST API | Profile stats and repos |
| LeetCode Stats API | Problem solving stats |
| Codeforces API | Rating and contest history |
| Groq API (Llama 3.3 70B) | AI assignment solver |

---

## 🏗️ Architecture 
┌─────────────────────────────────┐
│     React Frontend (Vercel)     │
│  Login · Dashboard · GPA · Jobs │
└────────────┬────────────────────┘
│ HTTPS + JWT Token
┌────────────▼────────────────────┐
│   Spring Boot Backend (Railway) │
│  REST APIs · JWT Filter · CORS  │
└────────────┬────────────────────┘
│
┌────────────▼────────────────────┐
│   PostgreSQL Database (Railway) │
│  Users · Semesters · Subjects   │
│  Job Applications               │
└─────────────────────────────────┘
│
┌────────────▼────────────────────┐
│        External APIs            │
│  GitHub · LeetCode · Codeforces │
│  Groq (Llama 3.3 70B)          │
└─────────────────────────────────┘
---

## 🚀 Running Locally

### Prerequisites
- Java 17+
- Node.js 20+
- PostgreSQL 17
- Maven

### Backend Setup

```bash
# Clone the repo
git clone https://github.com/yourusername/student-developer-dashboard.git
cd student-developer-dashboard/studentdashboard

# Create application.properties
cp src/main/resources/application.properties.example src/main/resources/application.properties

# Fill in your values
# spring.datasource.password=YOUR_POSTGRES_PASSWORD
# groq.api.key=YOUR_GROQ_KEY

# Create the database
psql -U postgres -c "CREATE DATABASE studentdashboard;"

# Run the backend
mvn spring-boot:run
# Backend runs on http://localhost:8080
```

### Frontend Setup

```bash
cd student-dashboard-frontend
npm install
npm run dev
# Frontend runs on http://localhost:5173
```

---

## 📡 API Reference

### Auth
| Method | Endpoint | Body | Description |
|--------|----------|------|-------------|
| POST | `/api/auth/register` | fullName, email, password, college, branch, year | Register |
| POST | `/api/auth/login` | email, password | Login → returns JWT token |

### GPA
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/gpa/semester` | Add semester |
| POST | `/api/gpa/subject` | Add subject with marks |
| GET | `/api/gpa/semesters/{userId}` | Get all semesters |
| GET | `/api/gpa/cgpa/{userId}` | Get CGPA |

### Jobs
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/jobs/add` | Add job application |
| PUT | `/api/jobs/status/{jobId}` | Update status |
| GET | `/api/jobs/list/{userId}` | Get all applications |
| DELETE | `/api/jobs/delete/{jobId}` | Delete application |

### Coding Profiles
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/github/stats/{username}` | GitHub profile |
| GET | `/api/leetcode/stats/{username}` | LeetCode stats |
| GET | `/api/codeforces/stats/{handle}` | Codeforces profile |

### AI Chatbot
| Method | Endpoint | Body | Description |
|--------|----------|------|-------------|
| POST | `/api/chatbot/ask` | question | Ask AI anything |

---

## 🗄️ Database Schema
users
├── id (PK)
├── fullName
├── email (unique)
├── password (BCrypt)
├── college, branch, year
├── githubUsername, leetcodeUsername, codeforcesUsername
└── createdAt
semesters
├── id (PK)
├── semesterName, semesterNumber
├── sgpa
└── user_id (FK → users)
subjects
├── id (PK)
├── subjectName
├── marksObtained, totalMarks, credits, gradePoints
└── semester_id (FK → semesters)
job_applications
├── id (PK)
├── companyName, role, status, notes
├── appliedAt
└── user_id (FK → users)
---

## 🧠 What I Learned Building This

- Designing and building REST APIs from scratch with Spring Boot
- Implementing JWT authentication with Spring Security filter chain
- JPA entity relationships (OneToMany, ManyToOne) with Hibernate
- Integrating multiple third party APIs in a production backend
- React component architecture and state management with hooks
- Axios interceptors for automatic JWT injection
- CORS configuration for cross-origin requests
- PostgreSQL database design and query optimization
- Deploying full-stack applications with Railway and Vercel

---

## 👨‍💻 Author

**Dhruv Gupta** — First year B.tech CSE Student  




<div align="center">
Built with ☕ Java and ⚛️ React
</div>
