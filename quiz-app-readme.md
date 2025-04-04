# Multiplayer Quiz Application

A real-time multiplayer quiz application that allows users to compete against each other in timed quiz matches. This application supports user registration, authentication, matchmaking, real-time gameplay, and leaderboard tracking.

## Features

- **User Authentication**: Secure signup and login with JWT authentication
- **Single-Player Mode**: Play solo with a 75-second time limit 
- **Multiplayer Mode**: Compete against other players in real-time with a 135-second time limit
- **Matchmaking System**: Queue-based system that pairs available players
- **Friend System**: Add friends, send/receive friend requests, and manage your friends list
- **Challenge System**: Create custom challenges with your own questions and answers
- **Leaderboards**: Track your ranking among other players in both single and multiplayer modes
- **Profile Statistics**: View your game history, win/loss records, and streaks
- **Real-time Updates**: Socket.IO implementation for live game state updates

## Technical Stack

- **Backend**: Node.js with Express
- **Database**: PostgreSQL
- **Real-time Communication**: Socket.IO
- **Authentication**: JWT (JSON Web Tokens)
- **Password Security**: bcrypt for hashing

## Prerequisites

- Node.js (v14 or higher)
- PostgreSQL database
- npm or yarn package manager

## Project Structure

```
.
├── .env                    # Environment variables
├── package.json            # Project dependencies
├── package-lock.json       # Dependency lock file
├── readme.md               # Project documentation
│
├── config/                 # Database configuration
│   ├── db.js               # Database connection setup
│   ├── db_fun.js           # Database query functions
│   └── profile_fun.js      # Profile statistics functions
│
├── controllers/            # Route controllers
│   ├── authController.js   # Authentication logic
│   ├── challengeController.js # Challenge system logic
│   ├── fedbckController.js # Feedback handling
│   ├── friendsController.js # Friend system logic
│   ├── leaderboardController.js # Leaderboard data
│   ├── profileController.js # User profile data
│   ├── quesController.js   # Question retrieval
│   ├── quiz1Controller.js  # Single-player game logic
│   └── quiz2Controller.js  # Multiplayer game logic
│
├── middleware/             # Middleware functions
│   └── authMiddleware.js   # JWT authentication middleware
│
├── routes/                 # API routes
│   ├── authRoutes.js       # Authentication routes
│   ├── challengeRoutes.js  # Challenge routes
│   ├── fedbckRoutes.js     # Feedback routes
│   ├── friendRoutes.js     # Friend system routes
│   ├── leaderboardRoutes.js # Leaderboard routes
│   ├── pingRoutes.js       # Connection verification routes
│   ├── profileRouter.js    # Profile routes
│   ├── quesRoutes.js       # Question routes
│   ├── quiz1Routes.js      # Single-player routes
│   └── quiz2Routes.js      # Multiplayer routes
│
└── src/                    # Source files
    └── server.js           # Main application entry point
```

## Setup Instructions

### 1. Clone the repository

```bash
git clone <repository-url>
cd quiz-application
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Create a `.env` file in the root directory with the following variables:

```
DATABASE_URL=postgresql://username:password@localhost:5432/quizapp
JSONTOKEN=your_secret_key_for_jwt
PORT=5000
```

### 4. Set up the database

Create a PostgreSQL database and tables according to the schema defined in the documentation. You'll need to create the following tables:

- topics
- users
- basicprofile
- friend
- friendreq
- frienddisplay
- isadmin
- lastlogin
- longeststreak
- dailystreak
- matchcount
- resultsummary
- userhistory1
- userhistory2
- feedback
- badge
- createchallenge
- sessionspec1
- sessionspec2

### 5. Start the server

```bash
npm start
```

The server will start on the port specified in your environment variables (defaults to 5000).

## API Endpoints

### Authentication

- `POST /auth/signup` - Register a new user
- `POST /auth/login` - Login a user

### Single-Player Quiz

- `POST /quiz1/start` - Start a single-player game
- `POST /quiz1/end` - End a single-player game and submit score

### Multiplayer Quiz

- `POST /quiz2/join` - Join the multiplayer waiting queue
- `POST /quiz2/leave` - Leave the multiplayer waiting queue

### Questions

- `GET /questions` - Get questions by topic ID

### Friend System

- `GET /friends/get_users` - Get list of available users
- `POST /friends/send_req` - Send a friend request
- `GET /friends/show_req` - Show received friend requests
- `POST /friends/accept_req` - Accept a friend request
- `POST /friends/reject_req` - Reject a friend request
- `GET /friends/get_friends` - Get list of friends
- `POST /friends/remove_friend` - Remove a friend

### Challenge System

- `POST /challenge` - Create a new challenge
- `GET /challenge/show` - Show challenges

### Feedback

- `POST /feedback` - Submit feedback

### Leaderboard

- `GET /leaderboard` - Get leaderboard data

### Profile

- `GET /profile` - Get user profile data

### Connection Verification

- `GET /ping` - Verify connection and token validity

## Game Flow

### Single-Player Mode

1. **Game Initiation**:
   - User authenticates
   - System generates a unique game ID
   - System randomly selects a topic and fetches questions

2. **Game Session**:
   - 75-second timer starts
   - User answers questions at their own pace

3. **Game Completion**:
   - Game ends when timer expires or user submits answers
   - Server saves game results
   - User's stats and leaderboard position are updated

### Multiplayer Mode

1. **Matchmaking**:
   - User joins the waiting queue
   - System pairs available players

2. **Game Setup**:
   - System creates a new game with a unique ID
   - System selects a topic and fetches questions

3. **Gameplay**:
   - Both players receive identical questions
   - 135-second timer starts
   - Players answer questions independently

4. **Game Completion**:
   - Game ends when both players submit scores, timer expires, or a player disconnects
   - Server calculates results and determines winner
   - Both players' stats are updated
   - 3-second cooldown before players can join new games

## Authentication

The application uses JWT (JSON Web Tokens) for authentication. After successful login, clients should:

1. Store the returned token
2. Include the token in the Authorization header for all protected routes:
   ```
   Authorization: Bearer <token>
   ```

## Socket.IO Events

For real-time communication, the application uses Socket.IO. Clients should listen for the following events:

- `connect` - Socket connection established
- `game_start` - A multiplayer game has started
- `game_end` - A multiplayer game has ended
- `disconnected` - Socket disconnection (handled by the server)

## Contributing

Please submit bug reports, suggestions, and pull requests to help improve this project.

## License

[Add your license here]
