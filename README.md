
# Open5GS + UERANSIM 5G StandAlone Simulation

This project sets up a full 5G Standalone (SA) Core with simulated UEs using UERANSIM.
It supports VoLTE-style bearer management, where:

- `ims` APN (QCI=5) is the default bearer for SIP signaling
- `internet` APN (QCI=1) is used for dedicated bearer with voice payload

# 📡 Open5GS + UERANSIM 5G SA & VoLTE Test Network

This project contains a complete 5G Standalone (SA) core network using Open5GS, along with UERANSIM to simulate UE and gNodeB functionality. Configured with Telia Finland’s MCC/MNC values (**244 / 91**) and supports VoLTE traffic simulation.

---

## 🔧 Components

| Service    | Description                            |
|------------|----------------------------------------|
| `AMF`      | Mobility & Access Management           |
| `SMF`      | Session Management (PDU, IP)           |
| `UPF`      | User Plane Data                        |
| `HSS`      | IMS & LTE Subscriber Data Management   |
| `PCF`      | Policy Control Function                |
| `UERANSIM` | Simulated UE + gNodeB                  |
| `MongoDB`  | Subscriber Data Storage                |
| `Grafana/Prometheus` | Monitoring (optional)       |

---

## 🛜 APN & QoS

| APN         | QCI / 5QI | Usage                               |
|-------------|-----------|-------------------------------------|
| `ims`       | 5         | SIP Signaling (VoLTE)               |
| `internet`  | 1         | Voice Data (VoLTE Payload)          |

---

## 📁 Project Structure



