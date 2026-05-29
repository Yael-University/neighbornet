# NeighborNet - Community Safety Social Network

**A location-based social platform connecting neighbors for community safety and engagement. Built with React Native, Node.js, and MySQL.**

[![React Native](https://img.shields.io/badge/React_Native-0.74+-61DAFB.svg)](https://reactnative.dev/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-green.svg)](https://nodejs.org/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0+-blue.svg)](https://www.mysql.com/)

---

## Overview

NeighborNet is a mobile-first social platform designed to:

1. **Connect neighbors** within geographic proximity for safety and community building
2. **Enable real-time communication** through direct messaging and group chats
3. **Facilitate local events** with location-based discovery and RSVP system
4. **Promote safety** through priority alerts and trusted contact networks

**Note:** This was a collaborative group project for Intro to Software Engineering. This repository represents the final production-ready version with contributions from the entire team.

## Key Features

### Social Networking
- User profiles with badges and achievements
- Follow system with mutual connections
- Post feed with media, comments, and likes
- Tag-based content filtering
- Real-time notifications

### Location-Based Services
- Event discovery within customizable mile radius
- Google Maps integration for event locations
- Distance-based post filtering
- Neighborhood-specific groups

### Communication
- Direct messaging (1-on-1 chat)
- Group messaging with roles (admin/moderator/member)
- Media sharing (images, voice messages)
- Message reactions and editing
- Real-time status indicators

### Safety Features
- Priority/urgent alert posts
- Trusted contact network
- Mutual follow requirement for messaging
- Location privacy controls
- Block/report functionality

### Gamification
- Achievement badges for community engagement
- Post history tracking
- User verification system

---

## Tech Stack

**Frontend:**
- **React Native** - Cross-platform mobile development
- **Expo** - Development platform and tools
- **TypeScript** - Type-safe JavaScript
- **React Navigation** - Navigation library
- **Socket.io Client** - Real-time communication
- **Google Maps API** - Location services

**Backend:**
- **Node.js** - Server runtime
- **Express.js** - Web framework
- **MySQL** - Relational database
- **Socket.io** - WebSocket server
- **Nodemailer** - Email verification
- **Multer** - File upload handling
- **JWT** - Authentication tokens

**DevOps:**
- **Production Backend** - Self-hosted with proxy manager
- **Expo Go** - Development testing platform

---

## System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    MOBILE CLIENTS                            │
│              (iOS/Android via Expo Go)                       │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           │ HTTPS + WebSocket
                           ▼
┌──────────────────────────────────────────────────────────────┐
│              NODE.JS BACKEND (Express + Socket.io)            │
│                                                               │
│  API Routes (150+ endpoints):                                │
│  ├── /api/auth/*        - Authentication & verification      │
│  ├── /api/users/*       - Profile management                 │
│  ├── /api/posts/*       - Post CRUD & interactions           │
│  ├── /api/feed/*        - Content feeds & search             │
│  ├── /api/events/*      - Event management & RSVPs           │
│  ├── /api/direct/*      - Direct messaging                   │
│  ├── /api/groups/*      - Group chats                        │
│  ├── /api/follows/*     - Follow system                      │
│  ├── /api/notifications/* - Push notifications               │
│  └── /api/badges/*      - Achievement system                 │
│                                                               │
│  Middleware:                                                 │
│  ├── auth.middleware.js - JWT validation                     │
│  ├── upload.middleware.js - File handling                    │
│  └── error.middleware.js - Error handling                    │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌──────────────────────────────────────────────────────────────┐
│                      MYSQL DATABASE                           │
│                                                               │
│  Core Tables:                                                │
│  ├── users           - User accounts & profiles              │
│  ├── posts           - User posts with media                 │
│  ├── comments        - Post comments                         │
│  ├── likes           - Post likes                            │
│  ├── events          - Community events                      │
│  ├── event_rsvps     - Event registrations                   │
│  ├── direct_messages - 1-on-1 chats                         │
│  ├── groups          - Group chats                           │
│  ├── group_messages  - Group chat messages                   │
│  ├── follows         - Follow relationships                  │
│  ├── trusted_contacts - Safety contacts                      │
│  ├── notifications   - User notifications                    │
│  └── badges          - Achievement system                    │
└──────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────┐
│                   EXTERNAL SERVICES                           │
│  ├── Google Maps API - Event locations & mapping             │
│  ├── Email Service - Verification emails                     │
│  └── File Storage - User uploads (profiles, posts, media)    │
└──────────────────────────────────────────────────────────────┘
```

---

## Installation & Setup

### Prerequisites
- Node.js 18+
- MySQL 8.0+
- Expo CLI
- iOS/Android device with Expo Go app

### Backend Setup

1. **Navigate to backend directory:**
```bash
cd NeighborNet-Personal/backend
```

2. **Install dependencies:**
```bash
npm install
```

3. **Configure environment:**
```bash
cp .env.example .env
# Edit .env with your database credentials
```

4. **Set up database:**
```bash
npm run setup-db
```

5. **Start backend server:**
```bash
npm start
```

Server will run on `http://localhost:3000` (or configured port)

### Frontend Setup

1. **Navigate to frontend directory:**
```bash
cd NeighborNet-Personal/frontend
```

2. **Install dependencies:**
```bash
npx expo install
```

3. **Configure backend URL:**
Edit `frontend/app/lib/config.ts`:
```typescript
export const BASE_URL = "http://YOUR_IP:3000";
```

4. **Start Expo development server:**
```bash
npx expo start
```

5. **Open in Expo Go:**
- Scan QR code with Expo Go app
- Ensure device is on same WiFi network as backend

---

## API Documentation

The backend provides **150+ RESTful endpoints** organized by feature:

### Authentication
- User registration with email verification
- Login with JWT tokens
- Password reset via email
- Username recovery

### Posts & Feed
- Create posts with media/location
- Comment and like system
- Tag-based filtering
- Priority alerts (last 24h)
- Location-based feed

### Events
- Create/manage community events
- Location selection via Google Maps
- RSVP system (going/interested/not going)
- Nearby events by radius
- Event attendee management

### Messaging
- Direct messaging (1-on-1)
- Group chats with roles
- Media sharing (images, voice, documents)
- Message reactions
- Read receipts
- Online status indicators

### Social Features
- Follow/unfollow users
- Mutual follow requirement for DMs
- User profiles with badges
- Achievement system
- Trusted contact network

### Notifications
- Real-time push notifications
- In-app notification center
- Unread count tracking
- Notification preferences

For complete API documentation, see the original NeighborNet README or explore `/backend/routes/`.

---

## Technical Highlights

### Scalability
- RESTful API design for horizontal scaling
- Database indexes for query optimization
- Connection pooling for concurrent users
- Efficient pagination for large datasets

### Security
- JWT-based authentication
- Email verification flow
- Password hashing with bcrypt
- Input validation and sanitization
- File upload size limits
- Role-based access control

### Real-Time Features
- Socket.io for live messaging
- Online status tracking
- Real-time notification delivery
- Typing indicators
- Message delivery receipts

### Performance
- Image compression for uploads
- Lazy loading for feed pagination
- Cached user sessions
- Optimized database queries with joins

---

## Database Schema

**Core entities and relationships:**

```sql
users (1) ──── (N) posts
users (1) ──── (N) events (as organizer)
users (N) ──── (N) users (follows, many-to-many)
users (N) ──── (N) events (RSVPs, many-to-many)
posts (1) ──── (N) comments
posts (1) ──── (N) likes
events (1) ──── (N) event_rsvps
users (N) ──── (N) users (direct_messages)
groups (1) ──── (N) group_members
groups (1) ──── (N) group_messages
users (1) ──── (N) notifications
users (1) ──── (N) badges
```

---

## Development Workflow

### Local Development
1. Start MySQL server
2. Run backend: `cd backend && npm start`
3. Run frontend: `cd frontend && npx expo start`
4. Test on Expo Go mobile app

### Production
- Backend hosted with proxy manager (internet-accessible)
- Frontend configured to connect to production backend
- Database hosted on production server

---

## Future Enhancements

- [ ] Implement end-to-end encryption for messages
- [ ] Add video call functionality
- [ ] Create web version (React)
- [ ] Implement advanced analytics dashboard
- [ ] Add content moderation AI
- [ ] Multi-language support
- [ ] Dark mode theme

---

## Project Context

This was developed as a final project for **Intro to Software Engineering** course. The goal was to create a production-ready mobile application that promotes community safety and engagement.

**Development Period:** Fall 2024  
**Team Size:** 6 developers  
**Platform:** React Native (iOS/Android)  
**Production Status:** Deployed with live backend

---

## Acknowledgments

Thank you to all team members for their contributions to this project:
- Brian Peredez (Backend/Database)
- Aidan Adame (Frontend Lead)
- Yael Mendez (Full-Stack)
- Jonathan Galvan (Frontend)
- Emerald Landry (Frontend/Design)
- Alawia Elgizouli (Design Documentation)

---

## License

This project is licensed under the MIT License.

---

## Contact

**Yael Mendez**  
- GitHub: [@yaelmendez](https://github.com/yaelmendez)
- LinkedIn: [Yael Mendez](https://linkedin.com/in/yaelmendez)
- Email: your.email@example.com

---

**Built for safer, more connected communities**
