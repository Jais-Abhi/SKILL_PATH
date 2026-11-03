# SkillPath AI

AI-powered learning platform that helps students build a personalized roadmap, track progress, resolve doubts with AI guidance, and discover project ideas and curated learning resources.

## Overview

SkillPath AI is a full-stack educational application designed for self-paced learners. Users create an account, answer a short onboarding form, and receive a personalized roadmap based on their learning goal, current skill level, and available weekly hours. The platform then helps them continue learning through:

- AI-generated roadmap steps
- AI chat support for questions and doubts
- Lesson and quiz generation for each learning topic
- Project recommendations based on level
- Resource discovery
- Progress monitoring and dashboard analytics
- Admin management for users and educational resources

## Features

### Student features
- User registration and login
- JWT-based authenticated sessions using HTTP-only cookies
- Learning goal onboarding workflow
- AI-generated roadmap with step-by-step milestones
- Dashboard with progress overview and learning stats
- AI chat assistant for contextual doubt-solving
- Lesson and quiz generation for each topic
- Project recommendations and saved project tracking
- Resource library with filters/search
- Profile management and learning progress tracking

### Admin features
- Admin dashboard with summary statistics
- User listing and status management
- Resource creation, update, and deletion
- Security controls for admin-only routes

## Tech Stack

### Frontend
- React 19
- Vite
- React Router DOM
- Axios
- Framer Motion
- Recharts
- React Markdown
- React Hot Toast
- React Icons

### Backend
- Node.js
- Express.js
- MongoDB
- Mongoose
- JWT
- Helmet
- CORS
- Express Rate Limit
- Morgan

### AI & Integration
- Groq SDK
- Llama 3.3 70B model
- Fallback roadmap/project generation when AI key is missing

## Project Flow

1. User signs up or logs in.
2. User completes onboarding with learning goal, level, and weekly hours.
3. Backend stores profile and uses AI to generate a personalized roadmap.
4. User sees dashboard summary and roadmap progress.
5. User can open AI chat, view learning lessons, and solve quizzes.
6. User receives project ideas and saves selected projects.
7. User browses curated resources and tracks completion.
8. Admin can manage users and resources from the admin panel.

## Core Modules

- Authentication and user management
- Profile onboarding and goal setup
- Roadmap generation and regeneration
- AI chat history and session support
- Learning lessons and quizzes
- Project recommendation engine
- Resource discovery
- Progress tracking
- Admin dashboard and resource management

## API Reference

Base URL:
- Backend: http://localhost:5000/api
- Frontend dev URL: http://localhost:5173

| Method | Endpoint | Description | Access |
| --- | --- | --- | --- |
| POST | /api/auth/register | Register a new user | Public |
| POST | /api/auth/login | Login and create auth cookie | Public |
| POST | /api/auth/logout | Clear JWT cookie | Public |
| GET | /api/auth/me | Get current user | Private |
| POST | /api/profiles | Create or update profile and generate roadmap | Private |
| GET | /api/profiles/me | Get user profile | Private |
| GET | /api/roadmaps/me | Get current roadmap | Private |
| POST | /api/roadmaps/regenerate | Regenerate roadmap | Private |
| POST | /api/chat | Send a message to AI chat | Private |
| GET | /api/chat/history | Get all chat sessions | Private |
| GET | /api/chat/history/:id | Get specific chat session | Private |
| GET | /api/projects/recommendations | Get project ideas | Private |
| POST | /api/projects/save | Save a project | Private |
| GET | /api/projects/saved | Get saved projects | Private |
| GET | /api/resources | Fetch curated learning resources | Private |
| POST | /api/learning/lesson | Generate AI lesson for a topic | Private |
| POST | /api/learning/quiz | Generate AI quiz for a topic | Private |
| GET | /api/admin/stats | Dashboard stats | Admin |
| GET | /api/admin/users | List all users | Admin |
| PUT | /api/admin/users/:id | Activate/deactivate a user | Admin |
| POST | /api/admin/resources | Add a resource | Admin |
| PUT | /api/admin/resources/:id | Update a resource | Admin |
| DELETE | /api/admin/resources/:id | Delete a resource | Admin |
| GET | /api/health | Health check | Public |

## Main Data Models

### User
- name
- email
- password
- role (`user` or `admin`)
- isActive
- timestamps

### Profile
- user
- learningGoal
- currentLevel
- weeklyHours

### Roadmap
- user
- goal
- level
- weeklyHours
- estimatedDuration
- steps
- aiGenerated

### Progress
- user
- roadmap
- completedSteps
- percentComplete
- streak

### ChatHistory
- user
- sessionId
- messages

### Resource
- title
- url
- type
- topic
- description
- tags
- addedBy

### SavedProject
- user
- title
- description
- difficulty
- techStack
- estimatedTime

## Project Structure

```text
skill-path/
├── backend/
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   │   ├── adminController.js
│   │   ├── authController.js
│   │   ├── chatController.js
│   │   ├── learningController.js
│   │   ├── profileController.js
│   │   ├── progressController.js
│   │   ├── projectController.js
│   │   ├── resourceController.js
│   │   ├── roadmapController.js
│   │   └── userController.js
│   ├── data/
│   │   └── fallbackRoadmaps.js
│   ├── middleware/
│   │   ├── authMiddleware.js
│   │   ├── errorMiddleware.js
│   │   └── rateLimiter.js
│   ├── models/
│   │   ├── ChatHistory.js
│   │   ├── Profile.js
│   │   ├── Progress.js
│   │   ├── Resource.js
│   │   ├── Roadmap.js
│   │   ├── SavedProject.js
│   │   └── User.js
│   ├── routes/
│   │   ├── adminRoutes.js
│   │   ├── authRoutes.js
│   │   ├── chatRoutes.js
│   │   ├── learningRoutes.js
│   │   ├── profileRoutes.js
│   │   ├── progressRoutes.js
│   │   ├── projectRoutes.js
│   │   ├── resourceRoutes.js
│   │   ├── roadmapRoutes.js
│   │   └── userRoutes.js
│   ├── services/
│   │   ├── aiService.js
│   │   └── fallbackService.js
│   ├── utils/
│   │   ├── generateToken.js
│   │   └── validators.js
│   ├── .env.example
│   ├── package.json
│   └── server.js
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── context/
│   │   ├── hooks/
│   │   ├── pages/
│   │   ├── routes/
│   │   ├── utils/
│   │   ├── App.css
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   ├── .env.example
│   ├── package.json
│   ├── vite.config.js
│   └── index.html
├── README.md
└── package.json
```

## Environment Variables

### Backend (.env)

```env
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb://127.0.0.1:27017/skillpath
JWT_SECRET=your_super_secret_key
GROQ_API_KEY=your_groq_api_key
CLIENT_URL=http://localhost:5173
```

### Frontend (.env)

```env
VITE_API_URL=http://localhost:5000/api
```

> If GROQ_API_KEY is not set, the app still works in fallback mode with prebuilt roadmap and project suggestions.

## Local Setup

### 1) Install dependencies

```bash
cd backend
npm install

cd ../frontend
npm install
```

### 2) Start backend

```bash
cd backend
npm run dev
```

### 3) Start frontend

```bash
cd frontend
npm run dev
```

### 4) Open the app

- Frontend: http://localhost:5173
- Backend API: http://localhost:5000/api/health

## Production Build

```bash
cd frontend
npm run build
```

Then run the backend in production mode:

```bash
cd backend
NODE_ENV=production npm start
```

The backend serves the production frontend build when `NODE_ENV=production` is enabled.

## Security and Architecture Notes

- JWT tokens are stored in HTTP-only cookies for authenticated requests
- CORS is restricted to configured frontend origins
- Helmet is enabled for HTTP header hardening
- Rate limiting is applied to auth endpoints
- Protected routes are guarded in the backend and frontend

## Roadmap and Future Enhancements

Possible next improvements include:
- user profile editing and onboarding updates
- roadmap step completion and persistence improvements
- richer analytics and streak tracking
- real resource tagging and search enhancements
- admin authentication onboarding and seeded admin users
- deployment to Vercel + Render or Railway

## License

This project is currently set up for internal development and learning purposes.

## Summary

SkillPath AI combines a modern React frontend with an Express + MongoDB backend and Groq-powered AI workflows to deliver a personalized learning experience. It is designed to help students learn faster, stay motivated, and move from beginner to job-ready through guided roadmaps, practical projects, and focused AI mentorship.
