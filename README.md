# Team Task Manager

A straightforward full-stack web application for managing team projects and tasks. I built this to solve the common problem of tracking who is working on what without the overhead of complex, bloated enterprise tools. It gives admins the ability to create projects and assign tasks, while team members can log in and update their progress.

## Features

- Authentication (Signup/Login)
- Role-based access (Admin/Member)
- Project creation and member management
- Task creation, assignment, and status updates
- Dashboard showing basic task stats
- Task deletion and project deletion (cascading deletes implemented)

## Tech Stack

- Frontend: React built with Vite
- Backend: Node.js with Express
- Database: MongoDB via Mongoose
- Auth: JWT stored in local storage
- Deployment: Designed for Railway

## Project Structure

The repository is split into two main directories:

- /server: Contains the Node.js backend. Organized into controllers, models, routes, and middleware to keep the business logic separated from routing.
- /client: Contains the React frontend. Organized into reusable components, pages, context for state management, and services for API calls.

## API Overview

The backend uses a standard REST pattern. Key endpoints include:

- Auth: Handles user registration and login. Returns a JWT that the client stores and sends back in headers for protected routes.
- Projects: Admins can create, edit, and delete projects. The endpoints filter data so users only see projects they are a part of.
- Tasks: Handles creating, assigning, updating, and deleting tasks. Regular members can only update the status of tasks assigned to them, while admins have full control.

## Setup Instructions

To run this locally, follow these steps:

1. Clone the repository
2. Install dependencies for both the frontend and backend:
   npm run install:all
3. Navigate to the server folder and create a .env file (see the Environment Variables section below).
4. Start the backend server:
   cd server
   npm start
5. In a separate terminal, start the frontend development server:
   cd client
   npm run dev

The app will be running at http://localhost:5173.

## Environment Variables

Create a .env file inside the /server directory with the following keys:

PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key

- PORT defines where the backend runs.
- MONGO_URI is your connection string to a local MongoDB instance or MongoDB Atlas.
- JWT_SECRET is used to sign the authentication tokens.

## Deployment

The application is structured to be deployed easily as a single service on Railway. 

The backend server is configured to check if it is running in production. If it is, it serves the compiled React frontend directly from the client/dist folder. When deploying to Railway, simply connect the repository and ensure the build script compiles the React app.

## Demo

Live URL: [Placeholder for live link]
Demo Video: [Placeholder for video link]

## Challenges & Learnings

Building this application under constraints brought up a few practical challenges:

- Time constraints: I had to prioritize core functionality and clean code over complex UI additions or heavily abstracted design patterns.
- Handling role-based access: Ensuring that members could not bypass the UI to perform admin actions required careful middleware checks on the backend, not just hiding buttons on the frontend.
- Managing relationships between models: Deleting a project leaves orphaned tasks in the database. I implemented cascade deletion in the project controller to ensure all related tasks are automatically removed when a project is deleted.
- Deployment issues: Setting up Vite's proxy for local development while ensuring the Express server correctly serves static files in production required a clean separation of environments.

## Future Improvements

If I had more time to work on this, I would add:

- Notifications when a user is assigned a new task
- Activity logs to track who updated a task's status
- Better UI elements like drag-and-drop boards for task management
- Real-time updates so team members don't have to refresh to see new tasks
