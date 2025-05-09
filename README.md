


# 📡 Open5GS + UERANSIM 5G SA & VoLTE Test Network

This project contains a complete 5G Standalone (SA) core network using Open5GS, along with UERANSIM to simulate UE and gNodeB functionality. Configured with MCC/MNC values (**999 / 01**) and supports VoLTE traffic simulation. This 5G SA test network runs entirely on ready-made configuration files and a Docker Compose setup.

# How does this environment work?

🧱 1. Docker Compose orchestrates the entire network

Command: docker-compose up -d

What it does:

Starts all services: open5gs, mongodb, ueransim, hss, pcf, smf, upf

Each component runs from a pre-built Docker image (e.g., open5gs/open5gs)

Configuration files like amf.yaml, smf.yaml, and ue0.yaml define the settings

📦 2. Configurations define network functionality

No custom Python/JavaScript/Go code

All settings live in *.yaml and *.json files

Examples:

smf.yaml: defines DNNs and IP ranges

ue0.yaml: specifies the UE’s IMSI and APNs

mongo/subscribers_*.json: contains subscriber entries for MongoDB

The test environment (Open5GS + UERANSIM) automatically builds tunneling during bearer setup using GTP-U (GPRS Tunneling Protocol – User Plane) and PFCP. Here’s a detailed description of what happens when a bearer is established and a tunnel is created:

📦 1. UE sends a PDU Session Establishment Request

The UERANSIM UE sends a PDU Session Establishment Request message to the AMF

The APN (DNN) determines the type of traffic (e.g., ims, internet)

🔄 2. AMF forwards the request to the SMF

The AMF passes the request over the SBI interface (N11) to the SMF

🧠 3. SMF selects a UPF and initiates tunneling

SMF chooses the UPF by its PFCP address (e.g., 127.0.0.7)

Uses PFCP (Packet Forwarding Control Protocol) over N4 to start the tunnel

text
Copy
Edit
SMF → UPF: PFCP Session Establishment Request
🌐 4. UPF creates the GTP-U tunnel

UPF replies with a PFCP Session Establishment Response

It sets up interfaces, for example:

ogstun (internet)

ogstun2 (ims)

It binds the PDU address (e.g., 10.244.0.2) into the tunnel

🔀 5. GTP-U user-plane traffic

UE and UPF exchange packets over GTP-U (UDP/2152)

The tunnel path looks like:

text
Copy
Edit
UE → gNB (UERANSIM) → UPF → ogstun/ogstun2 → DN (Data Network)
🧰 How this works in the test environment:

Component	Role
UERANSIM	Simulates the gNB and sends NAS + GTP signaling
SMF.yaml	Defines DNNs, IP ranges, and the UPF’s PFCP address
UPF.yaml	Configures the GTP-U IP, ogstun interface, and subnet settings
docker-compose.yaml	Launches SMF and UPF together in a compatible configuration


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

📦 final_open5gs_volte_project/
├── docker/
│ └── docker-compose.yaml
├── config/
│ ├── open5gs/
│ │ ├── amf.yaml
│ │ ├── smf.yaml
│ │ ├── upf.yaml
│ │ ├── hss.yaml
│ │ └── pcf.yaml
│ └── ueransim/
│ ├── ue0_telia.yaml
│ └── ue2_telia.yaml
├── mongo/
│ └── subscribers_multi_ims_internet_qos.json
├── .gitignore
└── README.md


## ▶️ Startup

```bash
cd docker
docker-compose up -d


Import MongoDB Data

mongoimport --db open5gs --collection subscribers --file ../mongo/subscribers_multi_ims_internet_qos.json --jsonArray

 Signaling & Data Flow
AMF handles registrations

SMF establishes PDU sessions

UPF creates ogstun and ogstun2 interfaces for the DNN

PCF can manage traffic paths based on QoS

IMS APN uses the default (signaling) bearer

Internet APN uses a separate bearer (data)


🔗 References
Open5GS: https://open5gs.org

UERANSIM: https://github.com/aligungr/UERANSIM

### Changes in configuration files of Open5GS 5GC C-Plane

The following parameters can be used in the logic that selects UPF as the connection destination by PFCP.

- DNN
- TAC (Tracking Area Code)
- nr_CellID

###
![image](https://github.com/user-attachments/assets/861d2af6-5792-460f-86e0-14400cf1a6b0)




