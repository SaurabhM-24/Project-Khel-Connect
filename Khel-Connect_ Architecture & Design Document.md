# 🏏 Khel-Connect: Architecture & Design Document (v1)

## 🔥 Highlights
- 🎯 **Single codebase** with React Native & Firebase.  
- 🤖 **AI-driven scoring** via Cloud Functions + MediaPipe.  
- ⚡ **Real-time leaderboards** with Firestore listeners.  
- 🔒 **Secure role-based access** for athletes & scouts.  
- 📈 **Future-ready** for multi-sport expansion.  

---

## 📑 Table of Contents
1. [System Architecture Overview](#1-system-architecture-overview)  
2. [High-Level Architectural Flow](#2-high-level-architectural-flow)  
3. [Component Breakdown](#3-component-breakdown)  
4. [API and Data Model](#4-api-and-data-model)  
5. [Security, Error Handling & Scalability](#5-security-error-handling--scalability)  
6. [Summary](#6-summary)  

---

## 1. System Architecture Overview
<details>
<summary>📌 Click to expand System Overview</summary>

Khel-Connect is built on a **modern, serverless, and event-driven architecture** designed for scalability, cost-effectiveness, and rapid development.  

- **Athlete App** → Cross-platform mobile app for video capture & profile management.  
- **Scout Dashboard** → Secure web portal for scouts to access leaderboards & analysis.  
- **AI Backend** → Serverless video-to-score pipeline powered by Firebase Cloud Functions.  

</details>

---

## 2. High-Level Architectural Flow
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
> 🔗 Replace ASCII with a **visual diagram** for presentations.

---

## 3. Component Breakdown

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Athlete App** (`khel-connect-app`) | React Native | User authentication, video uploads, profile & leaderboard view. |
| **Scout Dashboard** (`khel-connect-scout`) | React / Vue.js | Secure web portal for scouts to view athletes & leaderboards. |
| **Firebase Authentication** | Firebase | Manages athlete & scout accounts. |
| **Firebase Storage** | Firebase | Stores uploaded athlete videos. |
| **Firestore Database** | Firebase | Stores user profiles, video metadata & AI results. |
| **Firebase Cloud Functions** | Node.js/Python | Processes video → extracts metrics → generates Skill Score. |

---

## 4. API and Data Model

### 4.1 Firestore Data Model
<details>
<summary>📂 Click to expand Firestore Schema</summary>

#### Users Collection
- **Path**: `/users/{uid}`  
- **Document ID**: `uid` (from Firebase Authentication)  

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Full name |
| `email` | string | Email address |
| `location` | string | City/State |
| `sport` | string | Primary sport (default Cricket) |
| `role` | string | `athlete` or `scout` |

#### Videos Collection
- **Path**: `/videos/{documentId}`  
- **Document ID**: Auto-generated  

| Field | Type | Description |
|-------|------|-------------|
| `userId` | string | Reference to uploading user |
| `videoUrl` | string | Public Firebase Storage URL |
| `uploadTimestamp` | timestamp | Time uploaded |
| `status` | string | `processing`, `complete`, `failed` |
| `skillScore` | number | AI-generated performance score |
| `analysisMetrics` | map/object | e.g. `{ "armAngle": 90, "swingSpeed": 75 }` |

</details>

### 4.2 API Access (via Firebase SDK)
| Function | Purpose |
|----------|---------|
| `firebase.auth().signInWithEmailAndPassword()` | User login |
| `firebase.auth().signOut()` | Logout |
| `firebase.storage().ref(path).put(file)` | Upload video |
| `firebase.storage().ref(path).getDownloadURL()` | Get video URL |
| `firebase.firestore().collection('videos').add(data)` | Create video entry |
| `firebase.firestore().doc('videos/{docId}').update(data)` | Update with AI results |
| `firebase.firestore().collection('videos').orderBy('skillScore', 'desc').get()` | Leaderboard |
| `firebase.firestore().collection('videos').onSnapshot(snapshot)` | Real-time updates |

🔗 For full API reference → [See Khel-Connect API Documentation](Khel-Connect_API_Documentation.md)

---

## 5. Security, Error Handling & Scalability

### 🔒 Security
- Role-based access (athletes write-only, scouts read-only).  
- Firebase Security Rules for strict access control.  
- HTTPS + encrypted storage.  

### ⚠️ Error Handling
- Upload failure → mark as `failed` in Firestore.  
- AI error → set status `failed`, log details.  
- DB write failure → retry mechanism.  

### 📈 Scalability
- Serverless Cloud Functions auto-scale with load.  
- Modular AI pipelines → easy to extend to multiple sports.  
- Firestore indexes → optimized queries for leaderboards.  

---

## 6. Summary
Khel-Connect leverages **serverless architecture, AI-driven analysis, and Firebase’s scalable backend** to create a lightweight, secure, and extensible platform.  

✅ **Low-cost** → pay-per-use model.  
✅ **Real-time** → instant skill scoring & leaderboards.  
✅ **Future-ready** → supports expansion across multiple sports.  
