# College Feedback Management System

A full-stack MERN application for managing college feedback and reviews.

## Tech Stack

- **Frontend**: React 18, TailwindCSS, React Router
- **Backend**: Node.js, Express, MongoDB
- **Authentication**: JWT, bcryptjs
- **Deployment**: Vercel (Frontend + Serverless Backend)

## Project Structure

```
├── frontend/          # React frontend application
├── backend/           # Express.js backend API
├── api/               # Vercel serverless function entry point
└── vercel.json        # Vercel deployment configuration
```

## Local Development

### Prerequisites
- Node.js (v16 or higher)
- MongoDB (local instance or MongoDB Atlas)
- npm or yarn

### Setup

1. Clone the repository:
```bash
git clone https://github.com/ATS-DEVINE/College-Feedback-Management-System.git
cd College-Feedback-Management-System
```

2. Install dependencies:
```bash
# Install frontend dependencies
cd frontend
npm install

# Install backend dependencies
cd ../backend
npm install
```

3. Configure environment variables:
```bash
# Backend
cd backend
cp .env.example .env
# Edit .env with your MongoDB URI and JWT secret

# Frontend
cd ../frontend
cp .env.example .env.local
# Edit .env.local with your API URL
```

4. Start the development servers:
```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm start
```

The frontend will be available at http://localhost:3000
The backend API will be available at http://localhost:5000

## Deployment

### Vercel Multi-Service Deployment

This project is configured for deployment on Vercel using multi-service architecture, where the frontend and backend are deployed as separate services under a single project.

**Service Configuration:**
- **backend**: Express.js API service (internal, accessible via /api/* routes)
- **frontend**: React frontend service (public, handles all other routes)

**Routing:**
- `/api/*` → Routes to backend service
- `/*` → Routes to frontend service

**Service Bindings:**
- Frontend has a binding to backend via `BACKEND_URL` environment variable
- This allows the frontend to call the backend internally without exposing it publicly

### Deployment Steps

1. **Push to GitHub**:
   - Ensure your code is pushed to the GitHub repository

2. **Deploy to Vercel**:
   - Go to [vercel.com](https://vercel.com)
   - Click "Add New Project"
   - Import your GitHub repository
   - Vercel will automatically detect the `vercel.json` multi-service configuration
   - Click "Deploy"

3. **Configure Environment Variables in Vercel**:
   - Go to your project settings in Vercel
   - Navigate to Environment Variables
   - Add the following variables (apply to backend service):
     - `MONGODB_URI`: Your MongoDB connection string
     - `JWT_SECRET`: Your JWT secret key
     - `NODE_ENV`: production

4. **No Frontend Environment Variables Needed**:
   - The `BACKEND_URL` is automatically injected by Vercel via the service binding
   - For local development, you can still use `REACT_APP_API_URL` in `.env.local`

### Environment Variables

**Backend (.env)**:
```
MONGODB_URI=mongodb://localhost:27017/college-feedback
JWT_SECRET=your-secret-key
NODE_ENV=development
PORT=5000
```

**Frontend (.env.local)**:
```
REACT_APP_API_URL=http://localhost:5000/api
```

## Features

- User authentication (signup, login)
- College browsing and search
- Submit and manage reviews
- Admin dashboard for managing content
- Responsive design with TailwindCSS

## API Endpoints

- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/colleges` - Get all colleges
- `GET /api/colleges/:id` - Get college details
- `POST /api/reviews` - Submit a review
- `GET /api/reviews/college/:collegeId` - Get reviews for a college

## License

MIT
