---
title: "Khel-Connect: API Documentation"
---

# **1. Introduction**

Khel-Connect is an AI-powered sports talent discovery platform --- a
\'LinkedIn for Athletes.\' This document provides details of APIs and
data flows for mobile clients, scouts' dashboard, and backend AI
processing.\
\
The architecture is serverless and Firebase-centric. Instead of
traditional HTTP APIs, most interactions occur via Firebase SDKs (Auth,
Firestore, Storage). For clarity, we also provide equivalent REST-style
examples.

# **2. Authentication**

## **2.1 Athlete & Scout Authentication**

Authentication is managed via Firebase Authentication.\
Roles:\
- Athletes → read/write their own data, upload videos.\
- Scouts → read-only access to all athletes and video metadata.

  ---------------------------------------------------------------------------------------
  SDK Call                                            Description
  --------------------------------------------------- -----------------------------------
  firebase.auth().signInWithEmailAndPassword(email,   Sign in user with email/password
  password)                                           

  firebase.auth().signOut()                           Sign out current user

  firebase.auth().onAuthStateChanged(user)            Listen for authentication state
                                                      changes
  ---------------------------------------------------------------------------------------

REST Example (Login):

POST
https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=\<API_KEY\>\
Content-Type: application/json\
\
{\
\"email\": \"priya@example.com\",\
\"password\": \"mypassword\",\
\"returnSecureToken\": true\
}

## **2.2 Data Security**

\- Athletes: Can only access their own profile & videos.\
- Scouts: Read-only access to profiles, scores, leaderboards.\
- Enforced via Firebase Security Rules.

# **3. Storage API (Video Upload)**

Videos are stored in Firebase Storage.

  -----------------------------------------------------------------------------------
  SDK Call                                        Description
  ----------------------------------------------- -----------------------------------
  firebase.storage().ref(path).put(file)          Upload video to Firebase Storage

  firebase.storage().ref(path).getDownloadURL()   Retrieve public download URL
  -----------------------------------------------------------------------------------

Example Path Convention: /videos/{userId}/{timestamp}.mp4

# **4. Firestore Database API**

## **4.1 Data Models**

Users Collection (/users/{uid})

  -----------------------------------------------------------------------
  Field                   Type                    Description
  ----------------------- ----------------------- -----------------------
  name                    string                  Full name

  email                   string                  Email address

  location                string                  City/State

  sport                   string                  Primary sport (e.g.,
                                                  Cricket)

  role                    string                  athlete or scout
  -----------------------------------------------------------------------

Videos Collection (/videos/{videoId})

  -----------------------------------------------------------------------
  Field                   Type                    Description
  ----------------------- ----------------------- -----------------------
  userId                  string                  Uploader's uid

  videoUrl                string                  Download URL

  uploadTimestamp         timestamp               Upload time

  status                  string                  processing / complete /
                                                  failed

  skillScore              number                  AI score (0--100)

  analysisMetrics         map                     Metrics e.g.,
                                                  {armAngle: 145,
                                                  swingSpeed: 23.5}
  -----------------------------------------------------------------------

## **4.2 Core Data Operations**

  ------------------------------------------------------------------------------------------------------------------------------------
  SDK Call                                                                             Path                    Description
  ------------------------------------------------------------------------------------ ----------------------- -----------------------
  firebase.firestore().collection(\'videos\').add(data)                                /videos                 Add video metadata
                                                                                                               after upload

  firebase.firestore().doc(\'videos/{docId}\').update(data)                            /videos/{id}            Update processing
                                                                                                               results

  firebase.firestore().collection(\'videos\').where(\'userId\',\'==\',uid).get()       /videos                 Get all videos for user

  firebase.firestore().collection(\'videos\').orderBy(\'skillScore\',\'desc\').get()   /videos                 Get leaderboard
                                                                                                               (requires index)

 firebase.firestore().doc(\'users/{uid}\').get()                                      /users/{uid}            Get user profile
  ------------------------------------------------------------------------------------------------------------------------------------

# **5. Backend Triggers (Cloud Functions)**

\- Trigger: onFinalize event (when a new video is uploaded).\
- Steps:\
1. Extract frames (OpenCV)\
2. Pose estimation (MediaPipe)\
3. Apply custom metrics logic\
4. Compute skillScore & analysisMetrics\
5. Update Firestore document
