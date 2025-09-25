# Khel-Connect: API Documentation (v1)

## Highlights
- Built on Firebase SDKs for **Authentication, Firestore, and Storage**.  
- **Serverless Cloud Functions** handle AI video processing.  
- **Real-time** updates via Firestore listeners.  
- **Secure role-based access** for athletes and scouts.  
- Designed for **scalability and future multi-sport expansion**.  

---

## Table of Contents
1. [Authentication & Security](#1-authentication--security)  
2. [Storage API (Video Upload)](#2-storage-api-video-upload)  
3. [Firestore Database API](#3-firestore-database-api)  
   - [Data Models](#31-data-models)  
   - [Core Data Operations](#32-core-data-operations)  
4. [Backend Triggers (Cloud Functions)](#4-backend-triggers-cloud-functions)  
5. [Error Handling](#5-error-handling)  
6. [Versioning & Maintenance](#6-versioning--maintenance)  
7. [Summary](#7-summary)  

---

## 1. Authentication & Security
Authentication is managed by **Firebase Authentication**. Currently, the platform supports email/password login.  

| SDK Call | Description |
|----------|-------------|
| `firebase.auth().signInWithEmailAndPassword(email, password)` | Authenticate user login |
| `firebase.auth().signOut()` | Log out the current user |
| `firebase.auth().onAuthStateChanged(user)` | Listener for login state changes |

### Security Rules
- **Athletes**: Can read/write their own profile and upload videos.  
- **Scouts**: Read-only access to all profiles and video metadata.  
- **Rules**: Enforced using Firebase Security Rules and HTTPS for data integrity.  

For detailed Firebase Authentication documentation → [Firebase Auth Docs](https://firebase.google.com/docs/auth)  

---

## 2. Storage API (Video Upload)
Video uploads are handled via **Firebase Storage**.  

| SDK Call | Description |
|----------|-------------|
| `firebase.storage().ref(path).put(file)` | Upload video to a unique path in storage |
| `firebase.storage().ref(path).getDownloadURL()` | Get public URL for uploaded video |

For full Firebase Storage reference → [Firebase Storage Docs](https://firebase.google.com/docs/storage)  

---

## 3. Firestore Database API
The **Firestore Database** serves as the hub for user data, video metadata, and AI results.  

### 3.1 Data Models
<details>
<summary>Click to expand Firestore Schema</summary>

#### Users Collection
- Path: `/users/{uid}`  
- Document ID: `uid` (from Firebase Authentication)  

| Field | Type | Description |
|-------|------|-------------|
| name | string | Full name |
| email | string | Email address |
| location | string | City/State |
| sport | string | Primary sport (default: Cricket) |
| role | string | `athlete` or `scout` |

#### Videos Collection
- Path: `/videos/{documentId}`  
- Document ID: Auto-generated  

| Field | Type | Description |
|-------|------|-------------|
| userId | string | Reference to the user who uploaded the video |
| videoUrl | string | Public Firebase Storage URL |
| uploadTimestamp | timestamp | Upload time |
| status | string | `processing`, `complete`, `failed` |
| skillScore | number | AI-generated score |
| analysisMetrics | map/object | e.g., { armAngle: 90, swingSpeed: 75 } |

</details>

### 3.2 Core Data Operations
| SDK Call | Path | Description |
|----------|------|-------------|
| `firebase.firestore().collection('videos').add(data)` | `/videos` | Create a new video record |
| `firebase.firestore().doc('videos/{docId}').update(data)` | `/videos/{docId}` | Update with AI results |
| `firebase.firestore().collection('videos').where('userId', '==', uid).get()` | `/videos` | Fetch all videos for a user |
| `firebase.firestore().collection('videos').orderBy('skillScore', 'desc').get()` | `/videos` | Retrieve leaderboard (requires index) |
| `firebase.firestore().doc('users/{uid}').get()` | `/users/{uid}` | Retrieve user profile |
| `firebase.firestore().collection('videos').onSnapshot(snapshot)` | `/videos` | Real-time video status/results |

For complete Firestore documentation → [Firebase Firestore Docs](https://firebase.google.com/docs/firestore)  

---

## 4. Backend Triggers (Cloud Functions)
The AI pipeline runs on **Firebase Cloud Functions**.  

- **Trigger**: `onFinalize` event when a new video is uploaded.  
- **Process**: Extract frames → Pose estimation via MediaPipe → Calculate metrics → Generate Skill Score.  
- **Output**: Results written to Firestore.  

More on Cloud Functions → [Firebase Cloud Functions Docs](https://firebase.google.com/docs/functions)  

---

## 5. Error Handling
- **Video Upload Failure** → Status set to `failed` in Firestore.  
- **AI Processing Failure** → Status `failed`, log details for debugging.  
- **Database Write Failure** → Retry logic applied.  
- **Unauthorized Access** → Blocked via Firebase Security Rules.  

---

## 6. Versioning & Maintenance
- **API Version**: v1.0  
- **Last Updated**: September 2025  
- Future updates may include:  
  - Multi-sport analysis support.  
  - Expanded scout dashboard queries.  
  - Role-based advanced permissions.  

---

## 7. Summary
The **Khel-Connect API** integrates Firebase SDKs, Firestore, and Cloud Functions to deliver a secure, scalable, and real-time sports talent discovery platform.  

- Lightweight, serverless backend.  
- Real-time updates for athletes and scouts.  
- Secure and role-based by design.  
- Extensible to multiple sports.  
