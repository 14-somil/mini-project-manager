# Mini Project Manager

A full-stack project management application built with C# .NET 8 backend and React + TypeScript frontend. Users can create projects, manage tasks, and track completion status with JWT-based authentication.

## Features

- User authentication with JWT tokens
- Create, read, update, and delete projects
- Create, read, update, and delete tasks within projects
- Mark tasks as completed/incomplete
- Filter tasks by status (All, Active, Completed)
- Sort tasks by creation date, due date, or title
- Responsive UI with modern design
- In-memory data storage (no database setup required)

## Prerequisites

Before you begin, ensure you have the following installed:

- **.NET 8 SDK** - Download from [dotnet.microsoft.com](https://dotnet.microsoft.com/download)
- **Node.js 18+** - Download from [nodejs.org](https://nodejs.org)
- **npm** - Comes with Node.js

## Project Structure

\`\`\`
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
\`\`\`

## Backend Setup

### 1. Navigate to Backend Directory

\`\`\`bash
cd backend
\`\`\`

### 2. Restore Dependencies

\`\`\`bash
dotnet restore
\`\`\`

### 3. Run the Backend Server

\`\`\`bash
dotnet run
\`\`\`

The backend will start on `http://localhost:5000` and expose Swagger documentation at `http://localhost:5000/swagger`.

**Backend runs on:** `http://localhost:5000`

## Frontend Setup

### 1. Navigate to Frontend Directory

\`\`\`bash
cd frontend
\`\`\`

### 2. Install Dependencies

\`\`\`bash
npm install
\`\`\`

### 3. Run the Frontend Development Server

\`\`\`bash
npm run dev
\`\`\`

The frontend will start on `http://localhost:5173` (or another port if 5173 is in use).

**Frontend runs on:** `http://localhost:5173`

## Running Both Together

To run the full application:

1. **Terminal 1 - Backend:**
   \`\`\`bash
   cd backend
   dotnet run
   \`\`\`

2. **Terminal 2 - Frontend:**
   \`\`\`bash
   cd frontend
   npm run dev
   \`\`\`

3. Open your browser and navigate to `http://localhost:5173`

## API Endpoints

### Authentication

- `POST /api/v1/auth/register` - Register a new user
  \`\`\`json
  {
    "email": "user@example.com",
    "password": "password123",
    "username": "username"
  }
  \`\`\`

- `POST /api/v1/auth/login` - Login user
  \`\`\`json
  {
    "email": "user@example.com",
    "password": "password123"
  }
  \`\`\`

### Projects

- `GET /api/v1/projects` - Get all projects (requires auth)
- `GET /api/v1/projects/{projectId}` - Get project by ID (requires auth)
- `POST /api/v1/projects` - Create new project (requires auth)
  \`\`\`json
  {
    "title": "Project Name",
    "description": "Optional description"
  }
  \`\`\`
- `DELETE /api/v1/projects/{projectId}` - Delete project (requires auth)

### Tasks

- `GET /api/v1/projects/{projectId}/tasks` - Get all tasks in project (requires auth)
- `POST /api/v1/projects/{projectId}/tasks` - Create new task (requires auth)
  \`\`\`json
  {
    "title": "Task Name",
    "description": "Optional description",
    "dueDate": "2025-12-31"
  }
  \`\`\`
- `PUT /api/v1/projects/{projectId}/tasks/{taskId}` - Update task (requires auth)
  \`\`\`json
  {
    "title": "Updated Title",
    "isCompleted": true,
    "dueDate": "2025-12-31"
  }
  \`\`\`
- `DELETE /api/v1/projects/{projectId}/tasks/{taskId}` - Delete task (requires auth)

## Environment Variables

### Frontend

Create a `.env.local` file in the `frontend` directory (optional):

\`\`\`
VITE_API_URL=http://localhost:5000/api/v1
\`\`\`

If not set, defaults to `http://localhost:5000/api/v1`

### Backend

The backend uses in-memory storage by default. JWT secret key is set to a default value in development. For production, update the JWT secret in `Program.cs`.

## Usage Guide

### 1. Register/Login

- Navigate to the login page
- Click "Sign up" to create a new account
- Enter email, password, and username
- After registration, you'll be redirected to login
- Enter your credentials to access the dashboard

### 2. Create a Project

- Click "New Project" button on the dashboard
- Enter project title and optional description
- Click "Create" to save

### 3. Manage Tasks

- Click on a project to view its tasks
- Click "Add Task" to create a new task
- Enter task title, optional description, and due date
- Use the filter dropdown to view All, Active, or Completed tasks
- Use the sort dropdown to organize tasks by date or title
- Click the checkbox to mark tasks as complete
- Click the trash icon to delete tasks

### 4. Delete Projects

- Click the trash icon on a project card to delete it
- All associated tasks will be deleted

## Troubleshooting

### Backend won't start

- Ensure .NET 8 SDK is installed: `dotnet --version`
- Check if port 5000 is available
- Try: `dotnet clean` then `dotnet run`

### Frontend won't start

- Ensure Node.js 18+ is installed: `node --version`
- Delete `node_modules` and `package-lock.json`, then run `npm install`
- Check if port 5173 is available

### API connection errors

- Verify backend is running on `http://localhost:5000`
- Check browser console for error messages
- Ensure CORS is properly configured (should allow localhost:5173)
- Clear browser cache and localStorage

### Authentication issues

- Clear localStorage: Open DevTools → Application → Local Storage → Clear All
- Log out and log back in
- Check that JWT token is being stored in localStorage

### Tasks not appearing

- Refresh the page
- Verify you're logged in
- Check that the project ID in the URL matches an existing project
- Open browser DevTools to check for API errors

## Development Notes

- The backend uses in-memory database, so data resets when the server restarts
- JWT tokens are stored in browser localStorage
- All API requests require authentication except login/register
- CORS is configured to allow requests from localhost:3000 and localhost:5173

## Future Enhancements

- Persistent database (SQL Server, PostgreSQL, or SQLite)
- Task priorities and categories
- Task comments and attachments
- Team collaboration features
- Email notifications
- Task templates
- Advanced scheduling and analytics

## License

This project is provided as-is for educational purposes.
