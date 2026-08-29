# 🚨 AI-Based Voice Emergency Detection & Automatic Alert System

> An AI-powered emergency detection system that analyzes voice input, detects predefined emergency phrases, and automatically triggers an emergency alert with the user's location.

## 📌 Overview

During an emergency, a person may not be able to manually unlock their phone, open an application, make a call, or send an SMS.

This project aims to reduce that delay by providing an **automatic voice-based emergency detection system**.

The application captures voice input and uses **Faster-Whisper** for speech-to-text transcription. The transcribed speech is then analyzed for predefined emergency phrases such as:

* `Help`
* `Help me`
* `Emergency`
* `Save me`
* `Bachao`
* `Madad`
* `Bachao mujhe`
* `Madad karo`
* `कोई है`
* `बचाओ`
* `मदद करो`

When an emergency phrase is detected, the system automatically initiates the emergency alert workflow.

---

## 🎯 Problem Statement

In critical situations such as accidents, medical emergencies, or unsafe situations, a person may not have enough time or ability to manually operate their smartphone.

Traditional emergency systems generally require the user to:

1. Unlock the phone
2. Open an application
3. Select a contact
4. Make a call or send a message

This can cause valuable delays.

### Our Goal

To create an automated system that can detect an emergency through the user's voice and initiate an emergency alert with minimal or no manual interaction.

---

## 💡 Solution

The system combines:

* 🎙️ Voice input
* 🧠 AI-based speech recognition
* 🔎 Emergency phrase detection
* 📍 Location services
* 📱 Automatic SMS alerts
* 🔄 Retry handling
* ⚙️ Native Android background services

The overall workflow is:

```text
                 User Voice
                     ↓
              Audio Capture
                     ↓
          Faster-Whisper Model
                     ↓
            Speech-to-Text
                     ↓
         Emergency Phrase Detection
                     ↓
              Is Emergency?
                ↙       ↘
              NO         YES
              ↓            ↓
          Continue    Get User Location
                           ↓
                    Emergency Service
                           ↓
                    Send Alert / SMS
                           ↓
                  Emergency Contacts
```

---

## 🤖 How AI Is Used

The AI component uses **Faster-Whisper** to convert recorded speech/audio into text.

The system then analyzes the generated transcript and searches for predefined emergency phrases.

For example:

```text
User says:
"Please help me"

        ↓

Speech Recognition

        ↓

Transcript:
"please help me"

        ↓

Emergency Keyword Detection

        ↓

"help" detected

        ↓

🚨 Emergency Triggered
```

The backend uses the `faster-whisper` package with the **Whisper Tiny model** for speech transcription.

### Current AI Capability

The current implementation performs:

**Audio → Speech-to-Text → Emergency Phrase Detection**

It is currently **not a dedicated crying/emotion/distress-classification model**.

Future versions can extend the system with ML-based audio classification for signals such as crying, screaming, panic, or other distress patterns.

---

## ✨ Features

### 🎙️ Voice-Based Emergency Detection

Detects emergency phrases spoken by the user.

### 🧠 AI Speech Recognition

Uses Faster-Whisper to convert voice/audio into text.

### 🚨 Emergency Keyword Detection

Supports emergency phrases in English and Hindi, including phrases such as:

```text
Help
Emergency
Save me
Bachao
Madad
Bachao mujhe
Madad karo
बचाओ
मदद
मदद करो
```

### 📍 Location Support

The Android application includes location-handling functionality for retrieving the user's location during the emergency workflow.

### 📱 Automatic SMS Alert

The backend can send emergency SMS notifications through Twilio when an emergency phrase is detected.

### ⚙️ Native Android Services

The project includes native Android components for emergency handling, voice services, location, SMS, power-button interaction, and service communication.

### 🔄 Retry Mechanism

A retry manager is included to improve reliability when an emergency operation needs to be retried.

---

## 🏗️ System Architecture

```text
┌─────────────────────┐
│       User          │
│    Voice Input      │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   React Native App  │
│      + Expo         │
└──────────┬──────────┘
           │ Audio
           ▼
┌─────────────────────┐
│    Flask Backend    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Faster-Whisper    │
│   Speech-to-Text    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Emergency Keyword   │
│     Detection       │
└──────────┬──────────┘
           │
        Emergency
           │
           ▼
┌─────────────────────┐
│  Emergency Service  │
└───────┬───────┬─────┘
        │       │
        ▼       ▼
   Location    SMS
        │       │
        └───┬───┘
            ▼
    Emergency Contacts
```

---

## 🛠️ Tech Stack

### Mobile Application

* React Native
* Expo
* Java
* React Navigation

### AI / Speech Processing

* Faster-Whisper
* Python
* NumPy

### Backend

* Flask
* Python
* Gunicorn

### Communication

* Twilio SMS

### Mobile APIs / Services

* Expo Location
* Expo SMS
* Android Native Services

The current `package.json` uses Expo 54, React 19.1 and React Native 0.81.5, along with Expo Location and Expo SMS.

---

## 📂 Project Structure

```text
EmergencyAlertAutomation/
│
├── assets/
│
├── App.js
├── index.js
│
├── EmergencyPackage.java
├── EmergencyService.java
├── VoiceService.java
├── LocationHelper.java
├── SmsHelper.java
├── PowerButton.java
├── RetryManager.java
├── ServiceBridge.java
│
├── AndroidManifest.xml
│
├── app.py
├── server.js
│
├── package.json
├── package-lock.json
├── requirements.txt
│
├── app.json
├── eas.json
├── render.yaml
├── runtime.txt
├── .python-version
└── .gitignore
```

The repository currently contains separate Java components for emergency, voice, location, SMS, power-button and retry handling, along with the Flask backend and React Native/Expo application.

---

## 🔄 Emergency Detection Flow

### Step 1 — Voice Input

The user speaks an emergency phrase.

Example:

```text
"Help me"
```

### Step 2 — Audio Processing

The recorded audio is sent to the backend.

### Step 3 — Speech Recognition

Faster-Whisper converts the audio into text.

```text
Audio
  ↓
Whisper
  ↓
"Help me"
```

### Step 4 — Emergency Detection

The transcript is checked against predefined emergency phrases.

```text
"help me"
    ↓
"help" found
    ↓
Emergency = TRUE
```

### Step 5 — Alert

Once an emergency is detected, the system triggers the emergency alert workflow and can send an SMS notification through Twilio.

---

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/sagar-bharti/EmergencyAlertAutomation.git

cd EmergencyAlertAutomation
```

### 2. Install Node Dependencies

```bash
npm install
```

### 3. Install Python Dependencies

```bash
pip install -r requirements.txt
```

The backend dependencies currently include Flask, Faster-Whisper, NumPy, Gunicorn, Twilio and python-dotenv.

---

## 🔐 Environment Variables

**Never commit API keys, authentication tokens, phone numbers, or other secrets to GitHub.**

Create a `.env` file for sensitive configuration:

```env
TWILIO_SID=your_twilio_account_sid
TWILIO_TOKEN=your_twilio_auth_token
TWILIO_FROM=your_twilio_phone_number

EMERGENCY_CONTACT_1=your_emergency_contact
EMERGENCY_CONTACT_2=your_emergency_contact
```

For public repositories, provide a `.env.example` file instead of committing real credentials.

---

## ▶️ Running the Application

### Start the React Native / Expo Application

```bash
npm start
```

Or:

```bash
npm run android
```

The available npm scripts include Expo start, Android, iOS and web commands.

### Start the Flask Backend

```bash
python app.py
```

The backend exposes:

```text
GET  /health
POST /analyze
```

`/health` is used to check whether the service is running, while `/analyze` accepts an audio file for transcription and emergency analysis.

---

## 🧪 Example

### Input

```text
User:
"Bachao! Please help me!"
```

### Processing

```text
Voice
 ↓
Faster-Whisper
 ↓
Speech Transcript
 ↓
Emergency Keyword Detection
 ↓
"bachao" / "help" detected
 ↓
Emergency Trigger
```

### Output

```json
{
  "emergency": true,
  "keywords_found": ["help", "bachao"]
}
```

The backend returns the emergency status, transcript, detected language and matched keywords.

---

## 🔮 Future Improvements

The project can be extended with more advanced AI capabilities:

* 🤖 ML-based distress detection
* 😢 Crying detection
* 😱 Panic and screaming detection
* 🌐 Multi-language emergency detection
* 🧠 Context-aware emergency classification
* 🔇 False-positive reduction
* 📡 Real-time audio classification
* 🗺️ Live location tracking
* 👮 Integration with emergency response services
* ☁️ Cloud-based emergency monitoring
* 📊 Emergency event analytics

---

## ⚠️ Current Limitations

The current system primarily detects emergencies using **speech transcription and predefined emergency phrases**.

It does not currently perform dedicated emotion recognition or a trained crying/distress classification model.

This can be improved in future versions by training or integrating an audio classification model.

---

## 🔒 Security Note

This project handles sensitive information such as:

* Voice/audio data
* Location data
* Emergency contact information
* Communication credentials

Production deployment should use secure environment variables, encrypted communication, proper authentication, access control and secure storage of sensitive information.

---

## 🎥 Demo

> Add your project demonstration video here.

```text
[🎥 Watch Demo]
```

---

## 📱 Screenshots

Add screenshots of:

1. Home screen
2. Voice detection
3. Emergency detected
4. Location detection
5. Emergency SMS/alert

Example:

```text
## Home Screen

![Home Screen](assets/home-screen.png)

## Emergency Detection

![Emergency Detection](assets/emergency-detection.png)

## Emergency Alert

![Emergency Alert](assets/emergency-alert.png)
```

---

## 📌 Project Highlights

* AI-powered speech recognition
* Automatic emergency detection
* Voice-based interaction
* Hindi + English emergency phrases
* Automatic SMS notification
* Location support
* Native Android emergency services
* Flask backend
* React Native mobile application
* Retry mechanism for emergency operations

---

## 👨‍💻 Author

### Sagar Bharti

B.Tech Computer Science & Engineering

GitHub: [sagar-bharti](https://github.com/sagar-bharti)

---

## ⭐ Support

If you find this project useful, consider giving the repository a ⭐ on GitHub.

---

## 📄 License

This project is intended for educational and development purposes.
