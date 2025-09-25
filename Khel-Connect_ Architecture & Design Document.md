# Khel-Connect: Architecture & Design Document (v1)

## 1. Introduction & System Overview
Khel-Connect is built on a **modern, serverless, and event-driven architecture** designed for scalability, cost-effectiveness, and rapid development.  

At its core, the system leverages **Firebase services** with Cloud Functions to execute computationally intensive AI analysis without requiring a dedicated server.  

### Key Goals
- **Scalability**: Auto-scaling serverless backend for high video upload volumes.  
- **Cost-effectiveness**: Pay-per-use model with Firebase and Cloud Functions.  
- **Real-time Feedback**: Quick skill analysis and leaderboard updates.  
- **Security & Privacy**: Role-based access control with Firebase Authentication and Security Rules.  
- **Extensibility**: Modular design to add support for new sports and AI models.  

---

## 2. High-Level Architectural Flow

### Data Flow (Athlete → Scout)
```plaintext
+--------------------+       +--------------------+       +------------------------+ 
| Athlete Mobile App  | --->  | Firebase Storage    | --->  | Firebase Cloud Function | 
| (React Native)      |       | (Video Uploads)     |       | (AI Processing)         | 
+--------------------+       +--------------------+       +------------------------+ 
        |                                 ^                            | 
        | (Reads Score)                   |                            | (Writes to DB) 
        |                                 |                            | 
        |                                 +-------------------+        | 
        +-----------------------------> | Firestore Database | <------+ 
                                          +--------------------+ 
                                                    ^ 
                                                     | (Reads Data) 
                                                     | 
                                          +-------------------+ 
                                           | Scout Dashboard   | 
                                           | (Web App)         | 
                                           +-------------------+ 
```

> **Recommendation:** Replace ASCII diagram with a professional block diagram for final presentation.

---

## 3. Component Breakdown

### 3.1 Frontend Components

| Component | Technology | Purpose | Key APIs |
|-----------|------------|---------|----------|
| Athlete App (`khel-connect-app`) | React Native | Cross-platform mobile app for authentication, profile management, video upload, and viewing skill scores & leaderboards. | Firebase Authentication, Firebase Storage, Firestore |
| Scout Dashboard (`khel-connect-scout`) | React / Vue.js / Web Framework | Secure web portal for scouts to log in, view athlete profiles, leaderboards, and AI metrics. | Firebase Authentication, Firestore |

---

### 3.2 Backend & AI Components

| Component | Role | Details |
|-----------|------|---------|
| Firebase Authentication | Identity & Security | Manages user accounts (athletes & scouts). |
| Firebase Storage | Media Handling | Stores all uploaded video files securely. |
| Firestore Database | Data Hub | Stores user profiles, video metadata, and AI-generated results (Skill Score, metrics). |
| Firebase Cloud Functions | AI Processing | Triggered by video uploads, processes with MediaPipe/OpenCV, calculates metrics, and updates Firestore. |

---

## 4. AI Pipeline

### Step-by-Step Process
1. **Video Ingestion** → Cloud Function retrieves uploaded video from Firebase Storage.  
2. **Pose Estimation** → MediaPipe extracts key joint coordinates (shoulder, elbow, wrist, etc.) frame-by-frame.  
3. **Custom Metric Calculation** → Domain-specific algorithm calculates biomechanics (e.g., arm angle, swing speed).  
4. **Skill Score Generation** → Metrics combined into a final score.  
5. **Database Update** → Firestore updated with score & metrics; frontend displays results in real time.  

---

## 5. Data Model

### Users Collection
- **Path**: `/users/{uid}`  
- **Description**: Stores profile information for both athletes and scouts.  

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Full name of the user. |
| `email` | string | User’s email address. |
| `location` | string | City/State of the user. |
| `sport` | string | Primary sport (initially Cricket). |
| `role` | string | `athlete` or `scout`. |

### Videos Collection
- **Path**: `/videos/{documentId}`  
- **Description**: Stores metadata and AI analysis results for uploaded videos.  

| Field | Type | Description |
|-------|------|-------------|
| `userId` | string | Reference to the uploading user. |
| `videoUrl` | string | Public video URL in Firebase Storage. |
| `uploadTimestamp` | timestamp | When the video was uploaded. |
| `status` | string | Processing status: `processing`, `complete`, `failed`. |
| `skillScore` | number | AI-generated performance score. |
| `analysisMetrics` | map | Detailed breakdown (e.g., `{ "armAngle": 90, "swingSpeed": 75 }`). |

---

## 6. API Access (via Firebase SDK)

Instead of REST APIs, Khel-Connect relies on Firebase SDK calls.

| Function | Description |
|----------|-------------|
| `firebase.auth().signInWithEmailAndPassword(email, password)` | User login. |
| `firebase.auth().signOut()` | User logout. |
| `firebase.storage().ref(path).put(file)` | Upload video to storage. |
| `firebase.storage().ref(path).getDownloadURL()` | Retrieve video URL. |
| `firebase.firestore().collection('videos').add(data)` | Create new video entry. |
| `firebase.firestore().doc('videos/{docId}').update(data)` | Update video with AI results. |
| `firebase.firestore().collection('videos').orderBy('skillScore', 'desc').get()` | Get leaderboard. |
| `firebase.firestore().collection('videos').onSnapshot(snapshot)` | Real-time updates. |

---

## 7. Error Handling & Reliability

- **Video Upload Failure** → Mark status as `failed` in Firestore; notify user.  
- **AI Processing Failure** → Update document with `failed` status, log error for debugging.  
- **Database Write Failure** → Retry mechanism via Firebase SDK.  
- **Unauthorized Access** → Prevented via Firebase Security Rules.  

---

## 8. Security Considerations

- **Role-based Access Control (RBAC)** via Firebase Auth (athletes write-only for their data; scouts read-only access).  
- **Firebase Security Rules** restrict unauthorized reads/writes.  
- **Data Privacy** ensured by encrypted storage and HTTPS communication.  

---

## 9. Scalability & Extensibility

- **Serverless Scaling**: Cloud Functions auto-scale with upload volume.  
- **Future Sports Support**: Modular AI pipelines can be extended to football, basketball, etc.  
- **Leaderboard Optimization**: Firestore indexing for efficient queries.  
- **Monitoring**: Firebase Analytics + Cloud Logging for performance tracking.  

---

## 10. Summary

The **Khel-Connect Architecture** combines serverless design, AI-driven video analysis, and Firebase’s scalable backend.  

By separating frontend, backend, and AI responsibilities while keeping APIs lightweight, the system ensures:  
- Low-cost operation.  
- Real-time athlete evaluation.  
- Secure scout access.  
- Future-ready extensibility for multiple sports.  
