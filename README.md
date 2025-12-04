# AI-Powered Women Safety Smart Watch

This project builds an AI-enabled safety smartwatch that detects threats using
sound + motion + heart-rate patterns, and auto-activates safety features.

## ⭐ Key Features
- AI Threat Detection (shouting, fighting, abnormal motion)
- Auto SOS to nearest police station
- GPS Live Tracking
- 20-second audio & video recording upload
- Safe Defense Mode (non-harmful electric vibration)
- Mobile App Notifications
- Watch-to-Phone Bluetooth Sync

## 📌 Technologies Used
- Python (AI model)
- TensorFlow / PyTorch
- Arduino C++ (IoT firmware)
- Flask / FastAPI (Backend)
- Flutter (Mobile App)

## 📱 Mobile App Features
- SOS button
- Live location tracking
- Emergency contacts
- Threat alerts

## 🔗 How It Works
1. Sensors detect unusual sound/motion.
2. AI model classifies threat.
3. Watch vibrates & alerts user.
4. If no response → SOS auto-sends.
5. Police + contacts receive live location.

## 🔐 Safety
This project does NOT promote harmful weapons.
Only non-harmful self-defense vibration is used.
import tensorflow as tf
import numpy as np

class ThreatDetector:
    def __init__(self):
        self.model = tf.keras.models.load_model("threat_model.h5")

    def predict_threat(self, audio, motion):
        data = np.array([[audio, motion]])
        prediction = self.model.predict(data)
        return "THREAT" if prediction[0][0] > 0.7 else "SAFE"
#include <Wire.h>
#include <SoftwareSerial.h>

SoftwareSerial bt(10, 11); // Bluetooth TX RX

int vibrationPin = 6;
int micPin = A0;

void setup() {
  pinMode(vibrationPin, OUTPUT);
  Serial.begin(9600);
  bt.begin(9600);
}

void loop() {
  int soundLevel = analogRead(micPin);

  if (soundLevel > 650) {  
    digitalWrite(vibrationPin, HIGH);
    bt.println("THREAT_DETECTED");
    delay(3000);
    digitalWrite(vibrationPin, LOW);
  }
}
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.post("/sos")
def sos():
    data = request.json
    return {"message": "SOS received", "location": data['location']}

app.run(port=5000)
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.black,
      body: Center(
        child: ElevatedButton(
          onPressed: () {},
          style: ElevatedButton.styleFrom(
            backgroundColor: Colors.red,
            shape: CircleBorder(),
            padding: EdgeInsets.all(50),
          ),
          child: Text("SOS", style: TextStyle(fontSize: 30)),
        ),
      ),
    );
  }
}
┌─────────────────────────┐
│    🛡️ SAFETY WATCH      │
│                         │
│      ┌─────────┐        │
│      │   SOS   │        │
│      │  BUTTON │        │
│      └─────────┘        │
│                         │
│  📍 GPS  🎤 Mic  🎬 Cam │
└─────────────────────────┘
         ↓
┌─────────────────────────┐
│     MOBILE APP          │
│  Live Location Map      │
│  Emergency Contacts     │
│  Evidence Gallery       │
└─────────────────────────┘
         ↓
┌─────────────────────────┐
│     POLICE +            │
│  EMERGENCY CONTACTS     │
│  Get real-time alerts   │
│  with location & audio  │
└─────────────────────────┘
