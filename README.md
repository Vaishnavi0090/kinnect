# Kinnect

Kinnect is a full-stack activity discovery and social coordination platform designed to help users discover nearby activities, connect with people who share similar interests, and communicate through real-time messaging.

The platform combines location-aware activity discovery, activity-based group communication, direct messaging, friendships, notifications, and an emergency SOS mechanism into a unified web application.

---

## Features

### Activity Discovery

- Discover activities based on location and proximity
- View nearby activities through a location-aware activity feed
- Filter and explore activities based on user interests and preferences
- View detailed activity information
- Create, join, leave, and disband activities
- Support approval-based participation through join requests

### Interactive Map

- Visualize activities on an interactive map
- Display activity locations using map markers
- Select locations while creating activities
- Calculate proximity between users and activities for location-aware discovery

### Real-Time Communication

- Real-time activity group chat using WebSockets
- Activity-specific chat rooms
- Friend-to-friend direct messaging
- Conversation and message management

### Social Features

- Send and manage friend requests
- View user profiles
- Connect with other users through shared activities
- Receive notifications for relevant user and activity events

### User Authentication & Onboarding

- Google OAuth authentication
- Session-based authentication using NextAuth.js
- User onboarding and profile setup
- User profile management
- Interest and preference configuration

### Emergency SOS

- Location-aware SOS broadcasting
- Notify nearby users when an emergency is triggered
- Track emergency responses
- Allow users to respond to SOS alerts
- Support false-alarm reporting and validation
- Apply temporary account suspension after repeated false SOS alerts

---

## Tech Stack

### Frontend

- Next.js 14
- React 18
- JavaScript
- Tailwind CSS
- Framer Motion
- Leaflet
- React Leaflet
- SWR

### Backend

- Python
- FastAPI
- SQLAlchemy
- SQLite
- aiosqlite
- WebSockets

### Authentication

- NextAuth.js
- Google OAuth

---

## Architecture

Kinnect follows a client-server architecture with a Next.js frontend communicating with a FastAPI backend.

```text
                         ┌─────────────────────────┐
                         │      Next.js + React     │
                         │        Frontend          │
                         └────────────┬────────────┘
                                      │
                             HTTP / REST APIs
                                      │
                         ┌────────────▼────────────┐
                         │        FastAPI           │
                         │         Backend          │
                         └──────┬─────────┬────────┘
                                │         │
                       ┌────────▼───┐ ┌───▼──────────┐
                       │ SQLAlchemy │ │  WebSockets  │
                       │  + SQLite  │ │ Real-time    │
                       │  Database  │ │ Communication│
                       └────────────┘ └──────────────┘
```

---

## Project Structure

```text
## Project Structure

```text
kinnect/
│
├── backend/
│   ├── src/
│   │   ├── api/
│   │   │   ├── activities.py
│   │   │   ├── auth.py
│   │   │   ├── feed.py
│   │   │   ├── friends.py
│   │   │   └── sos.py
│   │   │
│   │   ├── models/
│   │   │   └── schema.py
│   │   │
│   │   ├── services/
│   │   │   └── db.py
│   │   │
│   │   ├── sockets/
│   │   │   ├── chat.py
│   │   │   └── dm.py
│   │   │
│   │   └── main.py
│   │
│   ├── migrate_db.py
│   ├── migrate_sos.py
│   ├── cleanup_notifs.py
│   ├── cleanup_all_notifs.py
│   ├── export_data.py
│   ├── render.yaml
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── ActivityCard.jsx
│   │   │   ├── ActivityInfoDrawer.jsx
│   │   │   ├── CalendarModal.jsx
│   │   │   ├── ChatsModal.jsx
│   │   │   ├── CreateFloatModal.jsx
│   │   │   ├── DirectMessageDrawer.jsx
│   │   │   ├── EmergencyModal.jsx
│   │   │   ├── FilterModal.jsx
│   │   │   ├── LiveChatDrawer.jsx
│   │   │   ├── LocationPicker.jsx
│   │   │   ├── MapFeed.jsx
│   │   │   ├── MyActivitiesModal.jsx
│   │   │   ├── NotificationsModal.jsx
│   │   │   ├── ProfileModal.jsx
│   │   │   ├── SOSAlertBanner.jsx
│   │   │   └── UserProfileModal.jsx
│   │   │
│   │   ├── pages/
│   │   │   ├── api/
│   │   │   │   └── auth/
│   │   │   │       └── [...nextauth].js
│   │   │   ├── dashboard.jsx
│   │   │   ├── index.jsx
│   │   │   ├── map.jsx
│   │   │   └── onboarding.jsx
│   │   │
│   │   ├── styles/
│   │   │   └── globals.css
│   │   │
│   │   └── utils/
│   │       └── feedback.js
│   │
│   ├── public/
│   │   ├── icon-512.png
│   │   ├── logo.png
│   │   ├── manifest.json
│   │   └── sw.js
│   │
│   ├── .env.example
│   ├── next.config.js
│   ├── package.json
│   ├── postcss.config.js
│   └── tailwind.config.js
│
├── .gitignore
├── README.md
└── package-lock.json
```
```

---

## Getting Started

### Prerequisites

Make sure the following are installed:

- Node.js
- npm
- Python 3.10+
- pip

---

## Installation

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd kinnect
```

### 2. Backend Setup

Create and activate a Python virtual environment:

```bash
python -m venv venv
```

#### Windows

```bash
venv\Scripts\activate
```

#### macOS / Linux

```bash
source venv/bin/activate
```

Install the backend dependencies:

```bash
pip install -r requirements.txt
```

### 3. Frontend Setup

Open a new terminal and install the frontend dependencies:

```bash
cd frontend
npm install
```

---

## Environment Variables

The application requires environment variables for authentication and backend configuration.

Create the required environment files using the provided example configuration.

### Frontend

Configure the required NextAuth.js and Google OAuth variables:

```env
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
NEXTAUTH_SECRET=your_nextauth_secret
NEXTAUTH_URL=http://localhost:3000
```

### Backend

Configure the backend API and application settings according to `.env.example`.

> **Note:** Never commit real credentials, API keys, OAuth secrets, or `.env` files to the repository.

---

## Running the Application

### Start the Backend

From the backend directory:

```bash
uvicorn src.main:app --reload
```

The FastAPI backend will run on the configured local backend port.

### Start the Frontend

From the frontend directory:

```bash
npm run dev
```

The Next.js development server will be available at:

```text
http://localhost:3000
```

---

## Application Modules

Kinnect is organized around several core application modules.

### Activities

The activity system supports:

- Activity creation
- Activity discovery
- Activity joining and leaving
- Join-request approval workflows
- Activity disbanding
- Activity participant management

### Feed & Location

The location-aware feed uses geographic coordinates to identify nearby activities and calculate distances between users and activities.

### Chat

The chat system provides:

- Activity-specific group conversations
- Real-time communication
- WebSocket-based message delivery
- Persistent message storage

### Direct Messaging

Users can communicate privately through:

- One-to-one conversations
- Friend-based messaging
- Persistent direct-message history

### Friends

The social graph supports:

- Sending friend requests
- Accepting or managing requests
- Maintaining user friendships
- Connecting with users through the platform

### Notifications

The notification system provides users with updates related to activities, friendships, messages, and other application events.

### SOS

The emergency system provides:

- Emergency creation with location information
- Location-aware notifications to nearby users
- SOS response tracking
- False-alarm validation
- Temporary suspension after repeated false SOS alerts

---

## Backend Components

The backend is organized into modular FastAPI components.

### Database Models

The database layer manages entities including:

- Users
- Activities
- Participants
- Join requests
- Chat messages
- Direct messages
- Friendships
- Notifications
- Emergency events

### API Modules

Dedicated backend modules handle:

- Authentication
- User management
- Activities
- Activity feed
- Friendships
- Notifications
- Group chat
- Direct messaging
- Emergency SOS functionality

### WebSockets

WebSocket endpoints provide real-time communication for:

- Activity group chats
- Direct messaging
- Live communication between connected users

---

## Development

The frontend uses reusable React/Next.js components and client-side data fetching, while the FastAPI backend provides modular REST APIs and WebSocket endpoints.

The application uses SQLAlchemy for database interaction and SQLite for local persistence.

---

## License

This project is intended for educational and portfolio purposes.
