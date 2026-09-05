# Iris — Household Voice Reminder Hub

## Status: In Progress 🚧

Iris is an ESP32-based shared voice assistant for the household. Anyone can walk up, say their name along with what they have going on, and later ask what everyone else has planned for the day.

## The Idea

- Say your name + a task/time ("This is Ally, I have a meeting at 6pm")
- Later, ask Iris what's going on today, or what a specific person has planned
- Shared, always-on device — no app, no login, just talk to it

## Current Approach

- ESP32 microcontroller
- Push-to-talk button trigger for now (wake-word detection is a stretch goal for later)
- Microphone → cloud speech-to-text API over WiFi
- Simple text parsing to extract name + task + time
- Local storage of reminders on-device
- Query mode reads back matching reminders

## Hardware (planned — not finalized)
- ESP32 dev board
- I2S microphone module
- (TBD: output method — speaker/TTS vs. small display)

## Roadmap
1. Get audio input working on the ESP32
2. Get WiFi + HTTP request working (send data out, get a response)
3. Combine audio capture + cloud speech-to-text, confirm transcription over serial
4. Add NTP time sync
5. Write the name/time/task parser
6. Build persistent storage for reminders
7. Build the query/read-back function
8. (Stretch) Add wake-word detection to replace the push-button

## Status Log
- [Date] — Repo created, project scoped, hardware not yet ordered

---
*This is a personal/independent project, built outside of coursework.*
