Khel-Connect: AI-Powered Platform for Democratizing Sports Talent🌟 

Project Overview
Khel-Connect is an AI-powered mobile and web platform designed to bridge the gap between undiscovered grassroots sporting talent and official scouting infrastructure in India. Our mission is to create a digital meritocracy for Indian sports, where an athlete's skill, not their background or location, determines their future.

The platform functions as a "LinkedIn for aspiring athletes," allowing them to create a digital portfolio and showcase their skills. Our core innovation is the AI Talent Scout, a feature that uses computer vision to analyze a player's performance from a simple video clip and provides an objective "Skill Score." This data feeds into a centralized dashboard for sports authorities, creating a new, unbiased channel for talent identification.

This project was developed for the SIH 2025 (Problem Statement: SIH25073 - Ministry of Youth Affairs and Sports).


✨ Key Features
* AI Talent Scout: The flagship feature that analyzes user-uploaded video clips of a specific sports action (e.g., a cricket bowl) and generates a quantified Skill Score based on key metrics like body posture, arm angle, and speed.
* Player Profiles: A digital sports portfolio where athletes can track their progress, view their Skill Scores, and maintain a showcase of their performance clips.
* Leaderboards: Dynamic, region-specific leaderboards that rank players based on their Skill Scores, promoting healthy competition and providing visibility to sports authorities.
* Scout Dashboard: A web portal for authenticated sports authorities to view and filter top-ranked players, analyze their profiles, and initiate the scouting process.


🛠️ Technology Stack
Khel-Connect is built on a modern, scalable, and cost-effective architecture.
Component  Technologies Used
Frontend   React Native
Backend    Firebase (Authentication, Firestore, Storage0)
AI/CV      MediaPipe, OpenCV
Cloud      Firebase Cloud Functions


🚀 Setup and Usage
Prerequisites
Node.js (v18 or higher)
React Native CLI
Firebase CLI

Installation
1. Clone the repository:
git clone [https://github.com/SaurabhM-24/Project-Khel-Connect.git](https://github.com/SaurabhM-24/Project-Khel-Connect.git)
cd khel-connect

2. Install dependencies:
# For the mobile app
npm install
# For the Firebase functions
cd functions
npm install

3. Set up Firebase:
* Create a new Firebase project and enable Firestore and Firebase Storage.
* Configure your project's Firebase credentials.
* Deploy the Cloud Functions from the functions directory:
  firebase deploy --only functions

4. Run the application:
# For Android
npx react-native run-android
# For iOS
npx react-native run-ios


🤝 Contribution Guidelines
We welcome contributions! Please follow these steps to get started:
1. Fork the repository and create a new branch for your feature or bug fix.
2. Follow the existing code style.
3. Write clear, concise commit messages.
4. Submit a Pull Request with a detailed description of your changes.For major features, please open an issue first to discuss the proposed changes.


📄 License
This project is licensed under the MIT License. See the LICENSE file for details.
