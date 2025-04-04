# 🎮 Multiplayer Quiz Application

A fast-paced, real-time multiplayer quiz platform where knowledge meets competition! Challenge yourself in solo mode or compete head-to-head against other players in exciting timed matches.



## ✨ Features

- **🔐 Secure Authentication** - Quick signup and login protected by JWT
- **🎯 Single-Player Mode** - Test your knowledge with a 75-second challenge
- **⚔️ Multiplayer Battles** - Face off against opponents in real-time (135-second matches)
- **🔍 Smart Matchmaking** - Get paired with available players instantly
- **👥 Social Features** - Add friends, send requests, and build your quiz network
- **🏆 Custom Challenges** - Create your own quizzes with custom questions and answers
- **📊 Global Leaderboards** - Track your ranking in both game modes
- **📈 Detailed Statistics** - Monitor your performance with comprehensive stats
- **⚡ Live Updates** - Experience real-time game state changes with Socket.IO

## 🛠️ Tech Stack

<div align="center">

| Technology | Purpose |
|------------|---------|
| **Node.js & Express** | Backend framework |
| **PostgreSQL** | Database management |
| **Socket.IO** | Real-time communication |
| **JWT** | Authentication |
| **bcrypt** | Password security |

</div>

## 📋 Prerequisites

- Node.js (v14+)
- PostgreSQL database
- npm or yarn package manager

## 📁 Project Structure

```
quiz-application/
│
├── 📄 .env                 # Environment configuration
├── 📦 package.json         # Dependencies and scripts
│
├── ⚙️ config/              # Database configuration
│   ├── db.js               # Connection setup
│   ├── db_fun.js           # Query functions
│   └── profile_fun.js      # User statistics
│
├── 🎮 controllers/         # Application logic
│   ├── authController.js   # Authentication
│   ├── quizControllers     # Game mechanics
│   └── ...                 # Other controllers
│
├── 🛡️ middleware/         # Request processors
│   └── authMiddleware.js   # JWT validation
│
├── 🛣️ routes/             # API endpoints
│   ├── authRoutes.js       # Auth endpoints
│   ├── gameRoutes          # Quiz endpoints
│   └── ...                 # Other routes
│
└── 🚀 src/                 # Core application
    └── server.js           # Entry point
```

## 🚀 Getting Started

### 1️⃣ Clone the repository

```bash
git clone <repository-url>
cd quiz-application
```

### 2️⃣ Install dependencies

```bash
npm install
```

### 3️⃣ Set up environment variables

Create a `.env` file with:

```
DATABASE_URL=postgresql://username:password@localhost:5432/quizapp
JSONTOKEN=your_secure_jwt_secret_key
PORT=5000
```

### 4️⃣ Database setup

Initialize your PostgreSQL database with the required tables:

<details>
<summary>📑 View Database Tables</summary>

- topics - Question categories
- users - User accounts and credentials
- basicprofile - User statistics
- friend - Friend relationships
- friendreq - Friend requests
- matchcount - Game statistics
- resultsummary - Win/loss records
- createchallenge - Custom quiz challenges
- sessionspec1/2 - Game session data
- And other supporting tables

</details>

### 5️⃣ Launch the server

```bash
npm start
```

Your quiz application will be running at `http://localhost:5000` (or your configured port)!

## 🔌 API Endpoints

### 🔑 Authentication
- `POST /auth/signup` - Create new account
- `POST /auth/login` - Access your account

### 🎲 Game Modes
- `POST /quiz1/start` - Begin single-player challenge
- `POST /quiz1/end` - Complete single-player game
- `POST /quiz2/join` - Enter multiplayer queue
- `POST /quiz2/leave` - Exit multiplayer queue

### 👥 Social Features
- `GET /friends/get_users` - Discover potential friends
- `POST /friends/send_req` - Send friend request
- `GET /friends/show_req` - View incoming requests
- `POST /friends/accept_req` - Accept request
- `POST /friends/reject_req` - Decline request
- `GET /friends/get_friends` - View your friends
- `POST /friends/remove_friend` - Remove friend

### 🏆 Stats & Data
- `GET /leaderboard` - View top players
- `GET /profile` - See your performance
- `GET /questions` - Access quiz questions
- `POST /challenge` - Create custom quiz
- `GET /challenge/show` - Browse challenges
- `POST /feedback` - Share your thoughts

## 🎮 Game Flow

### 🎯 Single-Player Experience

1. **Start Game** → System generates ID and selects random topic
2. **Play Quiz** → 75-second countdown begins, answer questions
3. **End Game** → Score is calculated and stats are updated

### ⚔️ Multiplayer Battle

1. **Join Queue** → Enter matchmaking system
2. **Match Found** → Get paired with another player
3. **Battle Begins** → Both players receive identical questions with 135-second timer
4. **Final Score** → Winner determined, leaderboards updated






