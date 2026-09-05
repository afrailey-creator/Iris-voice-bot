# Iris — Voice Messenger Bot

## Status: Planned

Iris is an ESP32-based shared household voice messenger. Anyone can walk up, say their name, and either leave a voice message for someone else in the house or check messages left for them.

## Why This Project

Named after Iris, the Greek messenger goddess — the whole point of this device is relaying messages between people. Built to learn real embedded systems integration: audio capture, cloud speech-to-text, WiFi, persistent storage, and a small display, all coordinated through a finite state machine.

## Conversation Flow

1. Person says "Hi Iris" (button press for now — real wake-word detection is a stretch goal)
2. Iris (pre-recorded prompt): "Hello, who is this?"
3. Person says their name — matched against a known household name list
4. Iris (pre-recorded prompt): "Would you like to check your messages or send one?"

**Check messages branch:**
- If 0 messages: Iris says so, ends session
- If 1+ messages: Iris says "You have [count] messages, from [plays each sender's recorded name clip]"
- Person names who they want to hear from — matched against the list of senders with pending messages
- Iris plays that sender's name clip, then the message audio
- Message marked "heard" — stays stored until the recipient explicitly says "delete message"

**Send message branch:**
- Iris: "Who would you like to send the message to?"
- Person says a name — matched against the household list
- Iris: "Okay, recording in progress"
- Person speaks their message
- Person says "Iris end message" — recording stops, message stored

5. Person says "Bye Iris" — Iris responds with a random pre-recorded farewell, returns to idle (button-listening state)

## Data Stored Per Message
- Sender name (text, for matching)
- Sender's name audio clip (for playback — reused from step 3, no speech synthesis needed)
- Recipient name (text, for matching)
- Message audio (the recording itself)
- Heard flag (true/false)
- Deleted immediately on explicit "delete message" command

## Hardware (planned — not yet ordered)
- ESP32 dev board
- INMP441 I2S microphone (digital audio in — avoids ADC/WiFi noise interference)
- MAX98357A I2S amplifier + small speaker (audio out, same bus type as the mic)
- SSD1306 OLED display (animated "eyes," open when listening / closed when idle)
- Push-to-talk button (temporary stand-in for wake-word detection)

## Design Decisions (and why)
- **Fixed conversation structure**, not open-ended natural language — turns an unsolved AI problem into deterministic pattern matching
- **Known household name list**, hardcoded — Iris matches spoken names against a fixed set rather than recognizing arbitrary names
- **No text-to-speech** — all of Iris's spoken output (prompts, farewells, sender names) is pre-recorded audio, selected/played based on state, never generated live
- **No calendar/reminder features in v1** — earlier concept, cut to keep scope realistic (see Future Ideas)
- **No per-person colored lights** — considered, dropped due to added hardware/wiring cost with low payoff versus just asking who's talking

## Roadmap
1. Get I2S audio input working on the ESP32
2. Get WiFi + HTTP request working (send audio, get text back from speech-to-text API)
3. Combine 1+2, confirm transcription round-trip over serial
4. Build the household name-matching logic
5. Build audio recording + storage (tagged with sender/recipient)
6. Build playback + heard/delete logic
7. Add OLED "eyes" tied to device state (idle/listening/recording)
8. Add pre-recorded prompt and farewell playback
9. Wire the full state machine together end to end
10. (Stretch) Real wake-word detection (replace push-button)
11. (Future idea, not in v1) Calendar/reminder feature with time parsing and text-to-speech

## Status Log
- [Date] — Project scoped, conversation flow and data design finalized. Hardware not yet ordered.

---
*This is a personal/independent project, built outside of coursework.*
