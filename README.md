# 🌟 Khel-Connect: AI-Powered Platform for Democratizing Sports Talent

> _Bridging the gap between hidden grassroots sports talent and official scouting infrastructure in India._

![repo size](https://img.shields.io/github/repo-size/SaurabhM-24/Project-Khel-Connect?color=00FF7F)
![license](https://img.shields.io/github/license/SaurabhM-24/Project-Khel-Connect?color=blue)
![contrib](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg)

---

## 📑 Table of Contents
- [📌 Overview](#-overview)
- [✨ Key Features](#-key-features)
- [🛠️ Tech Stack](#️-tech-stack)
- [🚀 Setup & Usage](#-setup--usage)
  - [🔧 Prerequisites](#-prerequisites)
  - [📥 Installation](#-installation)
  - [🔌 Firebase Setup](#-firebase-setup)
  - [▶️ Run the Application](#️-run-the-application)
- [📁 Architecture Diagram / Demo (Optional)](#-architecture-diagram--demo-optional)
- [🤝 Contribution Guidelines](#-contribution-guidelines)
- [📄 License](#-license)

---

## 📌 Overview

**Khel-Connect** is an **AI-powered mobile + web platform** — a “LinkedIn for Aspiring Athletes”. Players can:
- Create a **digital portfolio**
- Upload performance videos
- Receive an **AI-generated Skill Score**
- Compete on **leaderboards** and get noticed by scouts

🏆 Built for **Smart India Hackathon (SIH) 2025**  
📝 Problem Statement: **SIH25073 – Ministry of Youth Affairs and Sports**

---

## ✨ Key Features

- **AI Talent Scout** – Computer-vision-based Skill Score (pose, angles, speed).  
- **Player Profiles** – Digital sports portfolio with clips & scores.  
- **Leaderboards** – Region-specific leaderboards to surface talent.  
- **Scout Dashboard** – Web portal for sports authorities to discover players.

---

## 🛠️ Tech Stack

| Component             | Technology |
|-----------------------|------------|
| Frontend (Mobile)     | React Native (Expo) |
| Backend & DB          | Firebase (Auth, Firestore, Storage) |
| AI / CV Engine        | Python Cloud Functions, MediaPipe, OpenCV |
| Web Dashboard         | React / Vue.js |
| Deployment            | Firebase Cloud Functions, Expo EAS |

---

## 🚀 Setup & Usage

### 🔧 Prerequisites
- Node.js (v18+)
- React Native CLI (or Expo)
- Firebase CLI

---

### 📥 Installation

```bash
# clone (if not done above)
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

# mobile app deps
npm install

# firebase functions
cd functions
npm install

```
🔌 Firebase Setup

Create a Firebase project and enable:

Authentication

Firestore Database

Storage

Add Firebase config credentials to your app.

Deploy Cloud Functions:

firebase deploy --only functions

▶️ Run the Application

For Android:

npx react-native run-android


For iOS:

npx react-native run-ios

📁 Architecture Diagram / Demo (Optional)

You can showcase your system flow and demo with visuals:

Add images/GIFs in docs/images/

Reference them like:

![Architecture](./docs/images/architecture.png)


💡 Example ideas:

architecture.png → System architecture (User → Firebase → Cloud Function → Firestore → Dashboard)

demo.gif → Clip showing upload → AI analysis → leaderboard update

🤝 Contribution Guidelines

We ❤️ contributions!

Fork the repository.

Create a feature branch (git checkout -b feature/my-feature).

Commit changes (git commit -m "feat: add my feature").

Push to the branch (git push origin feature/my-feature).

Open a Pull Request.

For major changes, please open an issue first to discuss.

📄 License

This project is licensed under the MIT License.
See the LICENSE
 file for more details.

🎯 Khel-Connect turns raw practice into opportunity — let’s put every hidden player on the map.

