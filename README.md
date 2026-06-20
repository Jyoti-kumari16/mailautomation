# Mail Automation - AI-Powered Email Web Application

A full-stack MERN (MongoDB, Express.js, React.js, Node.js) application with AI-powered email automation, spam detection, smart replies, scheduling, and admin analytics.

## Features

### Core
- JWT-based user authentication (register/login)
- Send real emails via Gmail SMTP (Nodemailer)
- Email history with sent/received filtering
- Category filtering (Spam, Important, Normal)

### AI-Powered
- Email intent understanding
- Professional auto-reply generation (3 suggestions)
- Email categorization (Complaint, Query, Support, Feedback)
- Sentiment analysis (positive, negative, neutral, urgent)
- Multi-language translation support
- Spam detection (keyword + AI classification)
- Automatic priority detection (High, Medium, Low)

### Advanced
- Scheduled email sending
- Auto follow-up system
- Voice-to-email input (Web Speech API)
- Admin panel with analytics

### Security
- Password hashing with bcrypt
- JWT authentication
- Role-based access control (admin/user)

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React.js, React Router, Axios, CSS |
| Backend | Node.js, Express.js |
| Database | MongoDB, Mongoose |
| Email | Nodemailer (Gmail SMTP) |
| AI | OpenAI API (gpt-4o-mini) |
| Auth | JWT, bcryptjs |

## Project Structure

```
mailautomation/
├── backend/
│   ├── config/          # Database configuration
│   ├── controllers/     # Route handlers (MVC)
│   ├── middleware/       # Auth & authorization
│   ├── models/          # Mongoose schemas
│   ├── routes/          # API routes
│   ├── services/        # AI, mail, scheduler
│   ├── utils/           # Spam detector
│   └── server.js
├── frontend/
│   ├── src/
│   │   ├── components/  # Reusable UI components
│   │   ├── context/     # Auth context
│   │   ├── pages/       # Login, Register, Dashboard, Admin
│   │   ├── services/    # API client
│   │   └── styles/      # CSS stylesheets
│   └── index.html
└── README.md
```

## Setup Instructions

### Prerequisites
- Node.js (v18+)
- MongoDB (local or Atlas)
- Gmail account with App Password
- OpenAI API key

### 1. Clone and Install

```bash
# Backend
cd backend
npm install
cp .env.example .env
# Edit .env with your credentials

# Frontend
cd ../frontend
npm install
```

### 2. Configure Environment Variables

Edit `backend/.env`:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/mailautomation
JWT_SECRET=your_super_secret_jwt_key
JWT_EXPIRE=7d

SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_gmail_app_password

OPENAI_API_KEY=your_openai_api_key
CLIENT_URL=http://localhost:5173
```

**Gmail App Password:** Go to Google Account → Security → 2-Step Verification → App Passwords → Generate one for "Mail".

### 3. Start MongoDB

```bash
# If using local MongoDB
mongod
```

### 4. Run the Application

```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm run dev
```

Open **http://localhost:5173** in your browser.

### 5. First User = Admin

The first registered user automatically gets the **admin** role with full access to the admin panel.

## API Endpoints

### Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login |
| GET | `/api/auth/me` | Get current user |

### Emails
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/emails/send` | Send/schedule email |
| POST | `/api/emails/receive` | Simulate incoming email |
| GET | `/api/emails` | Get email history |
| GET | `/api/emails/:id` | Get email by ID |
| DELETE | `/api/emails/:id` | Delete email |
| POST | `/api/emails/ai/reply` | Generate AI replies |
| POST | `/api/emails/ai/analyze` | Analyze email |
| POST | `/api/emails/ai/translate` | Translate text |

### Admin (admin role required)
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/admin/users` | List all users |
| GET | `/api/admin/emails` | List all emails |
| GET | `/api/admin/analytics` | Get analytics |
| DELETE | `/api/admin/users/:id` | Delete user |
| PUT | `/api/admin/users/:id/role` | Update user role |

## Usage Guide

1. **Register** an account (first user becomes admin)
2. **Compose** emails with AI analysis before sending
3. **Schedule** emails for future delivery
4. **Enable follow-up** to auto-send reminders
5. **Use voice input** to dictate email content
6. **Simulate incoming emails** to test AI categorization and reply suggestions
7. **Filter** email history by Spam, Important, or Normal
8. **Admin panel** for monitoring users, emails, and analytics

## Notes

- Without OpenAI API key, the app uses intelligent fallback logic for AI features
- Without SMTP credentials, emails are simulated and stored in the database
- Scheduled emails and follow-ups are processed by a cron job every minute
- Voice input requires a browser that supports the Web Speech API (Chrome recommended)
