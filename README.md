
# Open5GS + UERANSIM VoLTE Simulation (Telia MCC 244 / MNC 91)

This project sets up a full 5G Standalone (SA) Core with simulated UEs using UERANSIM.
It supports VoLTE-style bearer management, where:

- `ims` APN (QCI=5) is the default bearer for SIP signaling
- `internet` APN (QCI=1) is used for dedicated bearer with voice payload

Run with Docker Compose. Subscribers are pre-configured in MongoDB import file.
