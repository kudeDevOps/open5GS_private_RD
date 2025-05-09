
# 📡 Open5GS + UERANSIM 5G SA & VoLTE Test Network

This project contains a complete 5G Standalone (SA) core network using Open5GS, along with UERANSIM to simulate UE and gNodeB functionality. Configured with Finland’s MCC/MNC values (**244 / 91**) and supports VoLTE traffic simulation.

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



