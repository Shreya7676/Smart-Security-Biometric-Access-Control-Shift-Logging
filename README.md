<h1 align="center">🔐 Smart Fingerprint-Based Security System</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-ESP32-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Connectivity-WiFi-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Firebase-Connected-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/OLED-Display-black?style=for-the-badge">
</p>

---

## 📸 Project Overview

A **Smart Security System** built using an **ESP32 microcontroller**, a **fingerprint sensor**, and **Wi-Fi-enabled real-time logging**. The system records access logs to **Firebase** and offers an **Admin Dashboard** for live monitoring of access attempts.

> 💡 Designed for secure and contactless door access, with visual feedback via OLED display and centralized logging via Firebase.

---

## 🧰 Features

✅ Fingerprint-based secure access  
✅ OLED display for real-time status updates  
✅ Real-time logging using Firebase  
✅ Admin Dashboard for live access log monitoring  
✅ Green/Red LED indicators for access feedback  
✅ Buzzer for audible access confirmation  
✅ Fingerprint enrollment via Serial Monitor  
✅ Manual input simulation mode for testing

---

## 🧠 System Boot Process

- 🔌 On boot:
  - ESP32 connects to the configured Wi-Fi network
  - Initializes fingerprint sensor, OLED display, buzzer, LEDs, and servo motor
  - OLED shows: `Smart Security System`

---

## 👆 Fingerprint Detection Workflow

1. ✅ **If a fingerprint match is found:**
   - OLED shows:
     ```
     Matched ID
     Access Granted
     ```
   - Green LED turns ON  
   - Buzzer sounds  
   - Servo unlocks the door (rotates)
   - Fingerprint ID + timestamp sent to Firebase
   - After a short delay, servo locks the door again

2. ❌ **If no fingerprint match is found:**
   - OLED shows:
     ```
     No Match Found
     Access Denied
     ```
   - Red LED flashes

---

## 🧑‍💻 Enrollment Mode (via Serial Monitor)

The system allows secure fingerprint registration through the Serial Monitor, ensuring only authorized users are added.

### 👣 How to Enroll a Fingerprint:

1. 🔐 **Open Serial Monitor** (baud: `115200`)  
2. 💬 **Type the command:*input*

3. 🛠️ **The system will prompt:**
- 👉 *Place finger...*
- 👉 *Remove finger...*
- 👉 *Place the same finger again...*

4. 💾 If enrollment is successful:
Now, this fingerprint is stored under the entered ID and can be used for access.

5. ❌ If there is an error (e.g., bad image, mismatch), the system will display appropriate error messages, and you can retry.

---

## 🧪 Input Mode (For Testing)

This optional mode allows manual testing without scanning fingerprints — useful during debugging or demonstrations.

### 📥 How to Use:

1. Type:
2. Enter simulated access commands: p1, p2
3. Type `exit` to return to normal fingerprint detection mode.

Each simulated access sends the fingerprint ID and a static timestamp to Firebase.

---

## 🧑‍💼 Admin Dashboard – Real-Time Access Monitoring

The **Admin Dashboard** is a web-based interface built on top of **Firebase Realtime Database**, where administrators can monitor all access events — whether from real fingerprints or test simulations.

### 🔍 Key Features:

| Feature              | Description |
|----------------------|-------------|
| 📡 **Live Sync**      | View access logs in real-time as data updates in Firebase |
| 🕵️ **User Monitoring** | Know who accessed the system using fingerprint ID |
| ⏱️ **Timestamps**     | Logs show the exact time of each access |
| 🧪 **Test Entries**    | Simulated entries (from `input` mode) also appear for tracking |
| 📊 **Clean UI**        | Designed for easy viewing, filtering, or exporting access logs |

### 📁 Firebase Data Format:

Each fingerprint access is stored like this in Firebase:
```json
"fingerprints": {
"p1": {
 "fingerprintID": 1,
 "timestamp": "2025-06-03T18:00:00Z"
},
"p2": {
 "fingerprintID": 2,
 "timestamp": "2025-06-03T18:05:22Z"
}
}
