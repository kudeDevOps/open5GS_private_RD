
# Open5GS + UERANSIM 5G StandAlone Simulation

This project sets up a full 5G Standalone (SA) Core with simulated UEs using UERANSIM.
It supports VoLTE-style bearer management, where:

- `ims` APN (QCI=5) is the default bearer for SIP signaling
- `internet` APN (QCI=1) is used for dedicated bearer with voice payload


# 📡 Open5GS + UERANSIM 5G SA & VoLTE Testiverkko

Tämä projekti sisältää täyden 5G SA -ydinverkon Open5GS:llä sekä UERANSIM-simulaattorin UE- ja gNodeB-toiminnallisuuksille. Konfiguroitu Telia Finlandin MCC/MNC-arvoilla (**244 / 91**) ja tukee VoLTE-liikenteen simulointia.

---

## 🔧 Komponentit

| Palvelu | Kuvaus |
|---------|--------|
| `AMF`   | Mobility & Access Management |
| `SMF`   | Session Management (PDU, IP) |
| `UPF`   | Käyttäjädata (User Plane) |
| `HSS`   | IMS & LTE-tilaajadatan hallinta |
| `PCF`   | Policy Control Function |
| `UERANSIM` | Simuloitu UE + gNodeB |
| `MongoDB` | Tilaajadatan tallennus |
| `Grafana/Prometheus` | Monitorointi (ei pakollinen) |

---

## 🛜 APN & QoS

| APN       | QCI/5QI | Käyttö               |
|-----------|---------|----------------------|
| `ims`     | 5       | SIP Signaling (VoLTE) |
| `internet`| 1       | Puhedata (VoLTE payload) |

---

## 📁 Projektirakenne

```
📦 final_open5gs_volte_project/
├── docker/
│   └── docker-compose.yaml
├── config/
│   ├── open5gs/
│   │   ├── amf.yaml, smf.yaml, upf.yaml, hss.yaml, pcf.yaml
│   └── ueransim/
│       ├── ue0_telia.yaml, ue2_telia.yaml
├── mongo/
│   └── subscribers_multi_ims_internet_qos.json
├── .gitignore
└── README.md
```

---

## ▶️ Käynnistys

```bash
cd docker
docker-compose up -d
```

### MongoDB-tietojen import:

```bash
mongoimport --db open5gs --collection subscribers --file ../mongo/subscribers_multi_ims_internet_qos.json --jsonArray
```

---

## 📊 Signaling & Datan kulku

- AMF käsittelee rekisteröinnit
- SMF avaa PDU sessionit
- UPF luo `ogstun` ja `ogstun2` -rajapinnat DNN:lle
- PCF voi hallita QoS:n perusteella polkuja
- IMS APN käyttää oletusyhteyttä (signaling)
- Internet APN käyttää erillistä beareria (data)

---

## 🔗 Referenssit

- Open5GS: [https://open5gs.org](https://open5gs.org)
- UERANSIM: [https://github.com/aligungr/UERANSIM](https://github.com/aligungr/UERANSIM)

---

✅ Voit nyt käyttää tätä kouluprojektiin, GitHub-julkaisuun tai kehityslaboratorioon!
