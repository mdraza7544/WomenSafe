# Women Safety and Security System – Email Alert Application

## Project Information
* **Student Name:** Krupa Nag
* **Course:** MCA
* **Semester:** 3rd Semester

---

## 📌 Project Overview
The **Women Safety and Security System** is a modern, web-based emergency application designed to improve personal safety. The system provides a fast, reliable, and accessible way for users to alert trusted emergency contacts during critical situations by sharing their real-time location via Email and WhatsApp. 

This project integrates a single-click SOS trigger with a secure authentication system, an intuitive dashboard, and emergency contact management.

## 🎯 Problem Statement
In emergency situations, individuals often lack the time to manually type out messages or explain their location. Traditional safety mechanisms rely on the user making phone calls, which can be difficult or impossible when under threat. A one-click, automated distress signaling mechanism is required to instantly notify trusted contacts with actionable location data.

## 🚀 Project Objective
To develop a responsive, accessible web application that:
1. Allows users to register securely and manage emergency contacts.
2. Triggers an automated SOS protocol with a single click or voice command.
3. Automatically fetches the user's geographical location.
4. Broadcasts the distress signal to saved contacts via Email and WhatsApp.
5. Maintains a historical log of all triggered alerts for future reference.

---

## 🔥 Key Features
- **🚨 One-Click SOS Activation:** Triggers an immediate distress sequence.
- **🎙️ Voice Trigger SOS:** Allows hands-free activation.
- **📍 Real-Time Location Tracking:** Uses the browser's Geolocation API to fetch precise coordinates.
- **✉️ Automated Email Alerts:** Sends immediate email distress signals using EmailJS.
- **💬 WhatsApp Integration:** Generates auto-filled WhatsApp messages with a Google Maps location link.
- **🔊 Emergency Alarm:** Plays a loud distress sound to deter threats and attract attention.
- **📇 Emergency Contact Management:** Add, edit, and delete trusted emergency contacts.
- **📊 Alert History:** Logs previous SOS triggers with timestamps and locations.
- **🌙 Dynamic UI:** Includes a responsive Light/Dark mode theme toggle.

---

## ⚙️ Technologies Used

### Frontend
- **HTML5** (Structure & Semantics)
- **CSS3** (Styling, Layout, Light/Dark Modes)
- **JavaScript (Vanilla ES6)** (Application Logic & DOM Manipulation)

### Backend & Cloud Services
- **Firebase Authentication** (Secure User Login & Registration)
- **Firebase Firestore** (NoSQL Database for User Data, Contacts, and History)
- **Firebase Cloud Functions** (Node.js 18 Backend Environment)

### APIs & Integrations
- **EmailJS API** (Email Delivery Service)
- **Twilio SDK** (Cloud Communications)
- **Geolocation API** (Browser-based Location Fetching)
- **Google Maps** (Location Routing & Visualization)

---

## 🧠 System Workflow

1. **User Registration & Login:** User authenticates via Firebase Auth.
2. **Setup Phase:** User inputs their emergency contacts (Name, Email, Phone Number).
3. **Emergency Trigger:** User presses the "SOS" button or uses the Voice Trigger.
4. **Data Fetching:** The system retrieves the user's GPS coordinates (Latitude & Longitude).
5. **Data Processing:**
   - The alert is logged securely in the Firestore Database (`sos_history`).
   - The application dispatches parallel requests to EmailJS to email all saved contacts.
   - A WhatsApp routing link is generated for immediate messaging.
   - The audio alarm is triggered locally.
6. **Resolution:** Contacts receive a distress message containing the user's details, exact coordinates, and a clickable Google Maps link to reach the user.

---

## 📁 Project Folder Structure

```text
SOS_Emergency_Safety_App/
│
├── public/                 # Frontend assets and logic
│   ├── index.html          # Authentication/Landing Page
│   ├── css/                # Stylesheets
│   │   ├── layout.css
│   │   ├── main.css
│   │   └── theme.css
│   ├── js/                 # Client-side Scripts
│   │   ├── auth.js
│   │   ├── contacts.js
│   │   ├── env-config.js
│   │   ├── firebase.js
│   │   ├── history.js
│   │   ├── navigation.js
│   │   ├── sos.js
│   │   └── theme.js
│   ├── pages/              # Application Views
│   │   ├── contacts.html
│   │   ├── dashboard.html
│   │   ├── history.html
│   │   └── settings.html
│   └── assets/             # Media and Audio
│       └── audio/
│           └── sos-alarm.mp3
│
├── functions/              # Backend Cloud Functions
│   ├── index.js            # Node.js Twilio & Firebase logic
│   ├── package.json        # Node dependencies
│   └── .env                # Backend Secrets (Twilio)
│
├── scripts/                # Utility Scripts
│   └── generate-client-config.js
│
├── firestore.rules         # Database Security Configuration
├── firestore.indexes.json  # Database Query Indexes
├── firebase.json           # Firebase Deployment Configuration
├── package.json            # Project Metadata
├── .gitignore              # Git ignored files
├── .env.example            # Environment variables template
└── README.md               # Project Documentation
```

---

## 🛠️ Installation & Setup Guide

### 1. Prerequisites
- [Node.js](https://nodejs.org/) installed
- A [Firebase](https://console.firebase.google.com/) account
- An [EmailJS](https://www.emailjs.com/) account
- A [Twilio](https://www.twilio.com/) account

### 2. Setup Environment Variables
Duplicate `.env.example` and rename it to `.env` in the root directory. Fill in your credentials:

```env
# Twilio Configuration
TWILIO_ACCOUNT_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_token
TWILIO_PHONE_NUMBER=your_twilio_phone

# Firebase Configuration
FIREBASE_API_KEY=your_firebase_api_key
FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
FIREBASE_PROJECT_ID=your_project_id
FIREBASE_STORAGE_BUCKET=your_project.firebasestorage.app
FIREBASE_MESSAGING_SENDER_ID=your_sender_id
FIREBASE_APP_ID=your_app_id
FIREBASE_MEASUREMENT_ID=your_measurement_id

# EmailJS Configuration
EMAILJS_PUBLIC_KEY=your_emailjs_public_key
EMAILJS_SERVICE_ID=your_emailjs_service_id
EMAILJS_TEMPLATE_ID=your_emailjs_template_id
```

### 3. Apply Configuration to Frontend
Run the configuration script to securely generate the `env-config.js` file for the frontend:
```bash
node scripts/generate-client-config.js
```

### 4. Setup Cloud Functions
```bash
cd functions
npm install
```

### 6. Run the Application
The frontend consists of static files and can be served using any local web server. For example:
```bash
npx serve public
```
Navigate to `http://localhost:3000` (or your assigned port) in your browser.

---

## 🔒 Security Considerations
- **No Hardcoded Secrets in Git:** Sensitive API keys are injected dynamically via `.env` files and `env-config.js`. These are ignored in `.gitignore`.
- **Database Rules:** Firestore is protected by `firestore.rules`, ensuring users can only read/write their own contacts and SOS history (`request.auth.uid == userId`).
- **Authentication:** Enforced via Firebase Web SDK.

---

## ⚠️ Limitations
- Requires an active internet connection to contact Firebase and EmailJS servers.
- Accurate tracking depends heavily on the user granting Location Permissions in the browser.
- WhatsApp requires the WhatsApp Web or Mobile app to be installed to handle the routing links.

---

## 🚀 Future Enhancements
- Implementation of a Progressive Web App (PWA) to allow installation on mobile devices.
- Offline SOS alerts using SMS fallback integrations via native Android/iOS APIs.
- Continuous real-time location streaming after the initial SOS is triggered.
- Integration with local emergency dispatch services (Police/Ambulance).

---
*Developed for MCA 3rd Semester Project Submission.*


## How to run the project : 
      npx serve public 