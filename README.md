# Khel-Connect: AI-Powered Platform for Democratizing Sports Talent

> *Bridging the gap between hidden grassroots sports talent and official scouting infrastructure in India.*

![Repo Size](https://img.shields.io/github/repo-size/SaurabhM-24/Project-Khel-Connect?color=00FF7F)  
![License](https://img.shields.io/github/license/SaurabhM-24/Project-Khel-Connect?color=blue)  
![Contributions](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)  
![Open Issues](https://img.shields.io/github/issues/SaurabhM-24/Project-Khel-Connect)  
![Closed Issues](https://img.shields.io/github/issues-closed/SaurabhM-24/Project-Khel-Connect)  

---

## Table of Contents

- [Overview](#overview)  
- [Key Features](#key-features)  
- [Tech Stack](#tech-stack)  
- [Setup & Usage](#setup--usage)  
  - [Prerequisites](#prerequisites)  
  - [Installation](#installation)  
  - [Firebase Setup](#firebase-setup)  
  - [Run the Application](#run-the-application)  
- [Architecture Diagram / Demo](#architecture-diagram--demo)  
- [Contribution Guidelines](#contribution-guidelines)  
- [License](#license)  

---

## Overview

**Khel-Connect** is an **AI-powered mobile + web platform** — a “LinkedIn for Aspiring Athletes”.  

Players can:  
- Create a **digital portfolio**  
- Upload performance videos  
- Receive an **AI-generated Skill Score**  
- Compete in **leaderboards** and get noticed by scouts  

**Built for:** Smart India Hackathon (SIH) 2025  
**Problem Statement:** SIH25073 – Ministry of Youth Affairs and Sports  

---

## Key Features

- **AI Talent Scout** – Computer-vision-based Skill Scoring (pose, angles, speed).  
- **Player Profiles** – Digital sports portfolio with clips & scores.  
- **Leaderboards** – Region-specific rankings to surface hidden talent.  
- **Scout Dashboard** – Web portal for sports authorities to discover players.  

---

## Tech Stack

**Frontend (Mobile):**  
![React Native](https://img.shields.io/badge/React%20Native-20232A?logo=react&logoColor=61DAFB)

**Backend & Database:**  
![Firebase](https://img.shields.io/badge/Firebase-ffaa00?logo=firebase&logoColor=white)

**AI / Computer Vision:**  
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)  
![OpenCV](https://img.shields.io/badge/OpenCV-27338e?logo=opencv&logoColor=white)  
![MediaPipe](https://img.shields.io/badge/MediaPipe-4285F4?logo=google&logoColor=white)

**Web Dashboard:**  
![React](https://img.shields.io/badge/React-20232A?logo=react&logoColor=61DAFB)  
![Vue.js](https://img.shields.io/badge/Vue.js-35495E?logo=vue.js&logoColor=4FC08D)

**Deployment:**  
![Firebase Functions](https://img.shields.io/badge/Firebase%20Functions-FFCA28?logo=firebase&logoColor=black)  
![Expo](https://img.shields.io/badge/Expo-000020?logo=expo&logoColor=white)  

---

## Setup & Usage

### Prerequisites
- Node.js (v18+)  
- React Native CLI (or Expo)  
- Firebase CLI  

---

### Installation
```bash
Clone repository
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

Install mobile app dependencies
npm install

Install Firebase functions dependencies
cd functions
npm install
```


---

### Firebase Setup

```
1. Create a Firebase project.  
2. Enable the following services:  
   - Authentication  
   - Firestore Database  
   - Storage  
3. Add Firebase config credentials to your app.  
4. Deploy Cloud Functions:
  firebase deploy --only functions

```


---

### Run the Application
```
For Android:  
  npx react-native run-android


For iOS:  
  npx react-native run-ios

```
---

## Architecture Diagram / Demo
```
You can showcase your system flow and demo with visuals.  

Add images/GIFs in `docs/images/` and reference them in your README:  

![Architecture](./docs/images System architecture (User → Firebase → Cloud Function → Firestore → Dashboard)
![Demo]( Clip showing upload → AI analysis → leaderboard update

```
---

## Contribution Guidelines
```
We welcome contributions.  

1. Fork the repository  
2. Create a feature branch:  
    git checkout -b feature/my-feature
3. Commit changes:
    git commit -m "feat: add my feature"
4. Push to the branch:
    git push origin feature/my-feature
5. Open a Pull Request  

For major changes, please open an issue first to discuss your ideas.
```
---

## License

This project is licensed under the MIT License.  
See the [LICENSE](./LICENSE) file for more details.



