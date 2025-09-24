# Video Recommendation Engine Documentation

## Overview
The **Video Recommendation Engine** is a FastAPI-based backend system designed to deliver **personalized motivational and wellness video content** to users. This system dynamically ranks videos based on user engagement, while also providing **cold-start recommendations** for new users who have no prior interaction history.

---

## Key Features

### 1. Personalized Recommendations
- User interactions (`view`, `like`, `inspire`, `rating`) are tracked.
- Each interaction type has a **weight** that contributes to a video score:
  - `view` = 1
  - `like` = 3
  - `inspire` = 4
  - `rating` = 2
- Videos are **sorted by score** to deliver a personalized feed.

### 2. Cold-Start Support
- New users receive recommendations based on **mood-category mapping**, even before any interaction.
- Predefined categories:
  - Motivation
  - Wellness
  - Health
  - Focus
- Each category has a set of **curated example videos**, ensuring immediate engagement.

### 3. Category-Based Feed
- Users can fetch videos filtered by category (`project_code` query parameter).
- Combines **cold-start mood-based recommendations** and **interaction-weighted scores**.

### 4. Randomized Interaction Simulation (Demo Mode)
- For demonstration purposes, random interactions are generated for existing users.
- This simulates **dynamic feed updates** in Postman or live testing.

### 5. FastAPI & OpenAPI Integration
- Automatic API documentation available at `http://127.0.0.1:8000/docs`.
- Supports **Swagger UI** for live testing of endpoints.

---

## Endpoints

### 1. Personalized Feed
**GET** `/feed/?username=<username>`

**Response Example:**
```json
{
  "username": "John",
  "recommended_videos": [
    {"id": 1, "title": "Motivational Video 1", "category": "Motivation", "score": 4},
    {"id": 2, "title": "Wellness Video", "category": "Wellness", "score": 2}
  ]
}

2. Category-Based Feed
GET /feed/category?username=<username>&project_code=<category>

Response Example:
{
  "username": "John",
  "category": "Motivation",
  "recommended_videos": [
    {"id": 1, "title": "Motivational Video 1", "score": 4},
    {"id": 2, "title": "Motivational Video 2", "score": 2}
  ]
}

System Architecture
1. Database (SQLite/PostgreSQL)
   Tables: users, videos, interactions
   Relationships: User ↔ Interaction ↔ Video
2. Recommendation Logic
   Weighted scoring system based on user interactions.
   Cold-start fallback using mood-category mapping.
3. FastAPI Server
   Dependency injection for DB sessions.
   Endpoints serve JSON for Postman or frontend integration.

Professional Advantages
   Supports instant user engagement with cold-start logic.
   Dynamic, interaction-driven personalized feed.
   Demo-ready: randomized interactions simulate real app behavior.
   Easy to extend to graph-based or neural network recommendations later.

Future Enhancements
1. Integrate real FLIC API for live user interactions.
2. Implement graph neural network or embedding-based video similarity.
3. Add pagination and caching for large datasets.
4. Add user authentication for secure API access.