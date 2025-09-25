# Khel-Connect: Requirements Document  
**Version:** 1.0  
**Last Updated:** Sept 2025  
**Team:** Shadow Minds | SIH 2025  

---

## Table of Contents
- [1. Introduction](#1-introduction)  
- [2. Functional Requirements](#2-functional-requirements)  
  - [2.1 Athlete Mobile App](#21-athlete-mobile-app)  
  - [2.2 Scout Dashboard](#22-scout-dashboard)  
- [3. Technical Requirements](#3-technical-requirements)  
- [4. Non-Functional Requirements](#4-non-functional-requirements)  
- [5. Use Cases](#5-use-cases)  
- [6. Constraints](#6-constraints)  
- [7. Glossary](#7-glossary)  
- [8. Requirements Traceability Matrix (RTM)](#8-requirements-traceability-matrix-rtm)  
- [9. References & Links](#9-references--links)  

---

## 1. Introduction  

### 1.1 Purpose  
Khel-Connect is a mobile and web-based platform to democratize sports talent identification in India. It leverages AI to provide fair, objective, and scalable talent assessment, enabling athletes from any background to be discovered by scouts and authorities.  

### 1.2 Scope  
The MVP focuses on **cricket** and specifically the **bowling action**. This validates the core technology and provides a demonstrable prototype for SIH 2025.  

---

## 2. Functional Requirements  

<details>
<summary><b>2.1 Athlete Mobile App</b></summary>

**User Stories**  
- Create a profile to showcase skills.  
- Upload short video clips for AI analysis.  
- Receive a Skill Score with performance feedback.  
- Track rankings on leaderboards.  

**Requirements**  
- **Registration & Profile**: Name, email, password, sport (cricket), role (bowler), location.  
- **Video Upload**: MP4 format, ≤ 20 MB, progress indicator during upload.  
- **AI Analysis**: Display Skill Score (0–100) within 30 seconds, with at least two metrics (e.g., arm angle, swing speed).  
- **Leaderboard**: Dynamic, filterable by district/state.  

**Priority**: Must-Have for MVP  
**Acceptance Criteria**: Upload-to-Score cycle < 30s; leaderboard updates < 10s.  

</details>

<details>
<summary><b>2.2 Scout Dashboard</b></summary>

**User Stories**  
- Log in securely to view top athletes.  
- Access leaderboards based on Skill Scores.  
- View player profiles and analyzed clips.  
- Review AI metrics for each video.  

**Requirements**  
- **Authentication**: Secure login, role-based access, pre-approved accounts only.  
- **Dashboard**: Clean leaderboard visualization, profile access with videos and Skill Scores.  

**Priority**: Must-Have for MVP  
**Acceptance Criteria**: Verified scouts only; dashboard loads < 2s.  

</details>

---

## 3. Technical Requirements
- **Architecture**: Serverless (Firebase + Google Cloud Functions).  
- **Mobile App**: React Native (Expo).  
- **Backend**: Firebase Auth, Firestore (NoSQL), Firebase Storage.  
- **AI/ML Engine**: Python Cloud Function with MediaPipe + OpenCV.  
- **Dashboard**: React/Vue.js, hosted on Netlify/Vercel.  

**Data Flow**  
