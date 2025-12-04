# EduVexa API Documentation

## Overview
EduVexa uses Next.js API routes with mock data storage. All endpoints are fully functional and tested.

## Authentication
Demo credentials for testing:
- Email: `demo@eduvexa.com`
- Password: `demo123`

Authentication is handled via localStorage tokens. Include the auth token in your requests.

---

## API Endpoints

### 1. Feed - Get All Reels
**GET** `/api/feed`

Returns a personalized feed of reels.

**Response:**
\`\`\`json
{
  "success": true,
  "data": [
    {
      "id": "1",
      "title": "React Hooks Explained",
      "description": "Master React Hooks in 60 seconds...",
      "thumbnail": "/react-hooks.jpg",
      "creator": { "name": "Sarah Chen", "followers": "25K", "avatar": "/diverse-avatars.png" },
      "tags": ["React", "JavaScript", "Web Dev"],
      "difficulty": "Intermediate",
      "duration": "1:00",
      "views": "45.2K",
      "likes": 3240,
      "comments": 156,
      "saves": 892,
      "summary": "React Hooks revolutionized functional components..."
    }
  ]
}
\`\`\`

---

### 2. Get Reel Details
**GET** `/api/reels/:id`

Retrieves detailed information about a specific reel.

**Parameters:**
- `id` (string, required): Reel ID

**Response:**
\`\`\`json
{
  "success": true,
  "data": {
    "id": "1",
    "title": "React Hooks Explained",
    ...
  }
}
\`\`\`

**Error:**
\`\`\`json
{
  "success": false,
  "error": "Reel not found"
}
\`\`\`

---

### 3. Upload Reel
**POST** `/api/reels/upload`

Upload a new reel with metadata. Returns the created reel.

**Request Body:**
\`\`\`json
{
  "title": "My Learning Video",
  "description": "A comprehensive guide to...",
  "tags": "React, JavaScript, Web Dev",
  "difficulty": "Intermediate",
  "videoUrl": "https://example.com/video.mp4"
}
\`\`\`

**Response:**
\`\`\`json
{
  "success": true,
  "message": "Reel uploaded successfully",
  "data": {
    "id": "1234567890",
    "title": "My Learning Video",
    "views": 0,
    "likes": 0,
    ...
  }
}
\`\`\`

---

### 4. Get Quiz Questions
**GET** `/api/quiz?reelId=1`

Retrieves practice quiz questions for a specific reel.

**Query Parameters:**
- `reelId` (string, required): Reel ID

**Response:**
\`\`\`json
{
  "success": true,
  "data": {
    "reelId": "1",
    "questions": [
      {
        "question": "What is the primary purpose of useState?",
        "options": [
          "To manage side effects",
          "To manage state",
          "To optimize performance",
          "To handle lifecycle"
        ],
        "correctAnswer": 1,
        "explanation": "useState allows functional components to have state..."
      }
    ]
  }
}
\`\`\`

---

### 5. Get Comments
**GET** `/api/comments?reelId=1`

Retrieves all comments for a specific reel.

**Query Parameters:**
- `reelId` (string, required): Reel ID

**Response:**
\`\`\`json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "reelId": "1",
      "author": "Sarah Chen",
      "text": "This is incredibly helpful!",
      "timestamp": "2025-01-01T12:00:00Z"
    }
  ]
}
\`\`\`

---

### 6. Add Comment
**POST** `/api/comments`

Adds a new comment to a reel.

**Request Body:**
\`\`\`json
{
  "reelId": "1",
  "author": "John Doe",
  "text": "Great explanation!"
}
\`\`\`

**Response:**
\`\`\`json
{
  "success": true,
  "message": "Comment added",
  "data": {
    "id": 2,
    "reelId": "1",
    "author": "John Doe",
    "text": "Great explanation!",
    "timestamp": "2025-01-01T12:30:00Z"
  }
}
\`\`\`

---

## Feature Checklist

### Authentication (✅ Implemented)
- Login with email/password
- Register new account
- Token-based auth with localStorage
- Protected routes redirect to login
- Logout functionality

### Video Playback (✅ Implemented)
- Autoplay with sound handling
- Play/Pause controls
- Mute/Unmute toggle
- Volume slider (0-100%)
- Progress tracking
- Single video playing at a time
- Browser autoplay blocking handled

### Dark Mode (✅ Implemented)
- Full dark theme support
- Light creme theme (#FBF7F2)
- Theme persistence via localStorage
- Toggle in navigation
- Applied to all components

### Edit Profile (✅ Implemented)
- Edit name and bio
- Save profile changes
- Changes persist in localStorage
- Modal interface

### AI Features (✅ Implemented)
- AI-generated summaries per reel
- Quiz questions with explanations
- AI Chatbot in settings
- Common question responses

### Backend APIs (✅ Implemented)
- GET `/api/feed` - Fetch reels
- GET `/api/reels/:id` - Reel details
- POST `/api/reels/upload` - Upload reel
- GET `/api/quiz?reelId=:id` - Quiz questions
- GET `/api/comments?reelId=:id` - Comments
- POST `/api/comments` - Add comment

---

## Testing the App

1. **Login**: Use demo@eduvexa.com / demo123
2. **View Feed**: Scroll through reels
3. **Open Reel**: Click any reel to open player
4. **Video Controls**: Test play, pause, volume, mute
5. **Dark Mode**: Toggle in navbar
6. **Quiz**: Click "Practice Quiz" button
7. **Edit Profile**: Go to Profile → Edit Profile
8. **Chatbot**: Profile → Settings → Chat with AI

---

## Notes
- All data is stored in localStorage (mock storage)
- Video uses public demo video when no URL provided
- Data persists during browser session
- Refresh page to reset data
