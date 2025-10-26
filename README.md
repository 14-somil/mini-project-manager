# 🗂️ Mini Project Manager

A full-stack project management application built with **C# .NET 8** backend and **React + TypeScript** frontend.  
Users can create projects, manage tasks, and automatically plan work schedules with a **Smart Scheduler API**, using secure **JWT-based authentication**.

---

## ✨ Features

- 🔐 User authentication with JWT tokens  
- 📁 Create, read, update, and delete projects  
- ✅ Create, read, update, and delete tasks within projects  
- 🕒 Mark tasks as completed/incomplete  
- 🔍 Filter and sort tasks (status, date, title)  
- 🧠 **Smart Scheduler API** to auto-plan tasks within a project  
- 📱 Responsive UI with modern design  
- 💾 In-memory data storage (no database setup required)

---

## ⚙️ Prerequisites

Before you begin, ensure you have the following installed:

- **.NET 8 SDK** — [Download here](https://dotnet.microsoft.com/download)
- **Node.js 18+** — [Download here](https://nodejs.org)
- **npm** — Comes with Node.js

---

## 🗂️ Project Structure

```
mini-project-manager/
├── backend/                    # C# .NET 8 API
│   ├── Controllers/           # API endpoints
│   ├── Models/                # Data models
│   ├── Services/              # Business logic
│   ├── DTOs/                  # Data transfer objects
│   ├── Data/                  # Database context
│   └── Program.cs             # Application setup
├── frontend/                  # React + TypeScript app
│   ├── src/
│   │   ├── pages/            # Page components
│   │   ├── components/       # Reusable components
│   │   ├── services/         # API integration
│   │   └── App.tsx           # Main app component
│   └── package.json
└── README.md
```

---

## 🚀 Backend Setup

```bash
cd backend
dotnet restore
dotnet run
```

The backend will start on **http://localhost:5000**  
Swagger docs: [http://localhost:5000/swagger](http://localhost:5000/swagger)

---

## 💻 Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The frontend will start on **http://localhost:5173**

---

## 🔄 Running Both Together

1. **Backend**
   ```bash
   cd backend
   dotnet run
   ```
2. **Frontend**
   ```bash
   cd frontend
   npm run dev
   ```
3. Open your browser → `http://localhost:5173`

---

## 📡 API Endpoints

### 🧩 Authentication

| Method | Endpoint | Description |
|:------:|:----------|:-------------|
| POST | `/api/v1/auth/register` | Register new user |
| POST | `/api/v1/auth/login` | Login existing user |

**Example — Register**
```json
{
  "email": "user@example.com",
  "password": "password123",
  "username": "username"
}
```

---

### 📁 Projects

| Method | Endpoint | Description |
|:------:|:----------|:-------------|
| GET | `/api/v1/projects` | Get all projects (auth required) |
| GET | `/api/v1/projects/{projectId}` | Get project by ID |
| POST | `/api/v1/projects` | Create new project |
| DELETE | `/api/v1/projects/{projectId}` | Delete project |

**Example**
```json
{
  "title": "Project Name",
  "description": "Optional description"
}
```

---

### ✅ Tasks

| Method | Endpoint | Description |
|:------:|:----------|:-------------|
| GET | `/api/v1/projects/{projectId}/tasks` | Get all tasks |
| POST | `/api/v1/projects/{projectId}/tasks` | Create new task |
| PUT | `/api/v1/projects/{projectId}/tasks/{taskId}` | Update task |
| DELETE | `/api/v1/projects/{projectId}/tasks/{taskId}` | Delete task |

**Example**
```json
{
  "title": "Task Name",
  "description": "Optional description",
  "dueDate": "2025-12-31"
}
```

---

### 🧠 Smart Scheduler API (Assignment 2 Enhancement)

This API helps users **auto-plan their tasks** within a project based on due dates and available work hours.

| Method | Endpoint | Description |
|:------:|:----------|:-------------|
| POST | `/api/v1/projects/{projectId}/schedule` | Generate optimized task schedule |

**Example Input**
```json
{
  "tasks": [
    { "title": "Design UI", "estimatedHours": 5, "dueDate": "2025-10-30" },
    { "title": "Implement Backend", "estimatedHours": 8, "dueDate": "2025-10-28" },
    { "title": "Integration Testing", "estimatedHours": 4, "dueDate": "2025-11-02" }
  ],
  "workHoursPerDay": 6
}
```

**Example Output**
```json
{
  "schedule": [
    { "task": "Implement Backend", "startDate": "2025-10-26", "endDate": "2025-10-27" },
    { "task": "Design UI", "startDate": "2025-10-28", "endDate": "2025-10-29" },
    { "task": "Integration Testing", "startDate": "2025-10-30", "endDate": "2025-10-30" }
  ],
  "totalDurationDays": 5
}
```

**Notes**
- Generates a plan based on due dates and estimated effort  
- Adds visual feedback and loading indicators in the frontend  
- Mobile-friendly UI and deployable setup (backend: Render, frontend: Vercel)

---

## ⚙️ Environment Variables

### Frontend (`.env.local`)
```bash
VITE_API_URL=http://localhost:5000/api/v1
```

### Backend
- Uses in-memory storage by default  
- JWT secret defined in `Program.cs` (update for production)

---

## 🧭 Usage Guide

1. **Register/Login**
   - Sign up or log in to get JWT token
2. **Create a Project**
   - Add a title and optional description
3. **Add and Manage Tasks**
   - Create tasks, mark complete/incomplete, filter/sort them
4. **Use Smart Scheduler**
   - Click “Auto Schedule” to generate task plan
5. **Delete Projects**
   - Removes all associated tasks

---

## 🧱 Troubleshooting

- Ensure backend (`dotnet run`) and frontend (`npm run dev`) are both running  
- Check CORS settings if API calls fail  
- Clear browser cache/localStorage if authentication issues occur  

---

## 🧩 Development Notes

- Backend uses in-memory data — resets on restart  
- JWT tokens stored in browser `localStorage`  
- CORS allows requests from `localhost:3000` and `localhost:5173`  
- Smart Scheduler runs fully on backend logic  

---

## 🚧 Future Enhancements

- Persistent database (SQL Server / PostgreSQL / SQLite)  
- Task priorities, categories, and analytics  
- Team collaboration & comments  
- **AI-based Scheduler v2** for smarter rescheduling  
- Email notifications  

---

## 🪪 License

This project is provided **as-is for educational purposes**.