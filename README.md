# 🛡️ IoT Network Intrusion Detection System (NIDS)

This project presents a **modular, real-time Intrusion Detection System (IDS) simulator for IoT networks**, integrating signature-based, anomaly-based, and deep learning-based threat detection techniques. It provides an interactive interface for visualizing network activity and simulating cyber attacks in a safe, educational environment.

---

## 📌 Features

- 🧠 **Multiple Detection Models**:
  - Signature-based detection using `RandomForestClassifier`
  - Anomaly detection via `IsolationForest`
  - Deep Learning (CNN/RNN-based placeholder)
  - Ensemble voting mechanism for final decisions

- 📊 **Real-Time Dashboard & Visualization**:
  - Packet event scatter plots
  - Attack trend statistics
  - Event logs with color-coded alerts

- ⚠️ **Alert System**:
  - Customizable thresholds per attack type
  - Visual & in-app notifications
  - Extensible to support emails, SIEMs, and auto-responses

- 🧪 **Simulation & Real Network Support**:
  - Switch between simulated traffic and live packet capture
  - Adjustable simulation speed and sensitivity

- 🔧 **Extensibility**:
  - Easily add new models or visualizations
  - Integrate with external systems (e.g., firewalls, SIEM)

---

## 📐 System Architecture

[Packet Capture]
      ↓
[Feature Extraction]
      ↓
[Detection Models: Signature / Anomaly / DL]
      ↓
[Ensemble Decision Engine]
      ↓
[Notification System] ← [Visualization / Event Logs]

---

## 🧰 Core Components

| Component           | Description |
|---------------------|-------------|
| `PacketCapture`     | Simulates or captures real network traffic and extracts features |
| `IDSModels`         | Manages all detection algorithms and returns results |
| `SimulationWindow`  | Main PyQt GUI window with dashboards and controls |
| `NotificationSystem`| Triggers and manages alerts |

---

## 🚀 Getting Started

### ✅ Prerequisites

- Python 3.6+
- Install dependencies:

pip install PyQt5 pyqtgraph scikit-learn numpy pandas  
pip install scapy  


### 📦 Installation

git clone https://github.com/gohilmukund123/IoT-based-IDS.git  
cd IoT-based-IDS  
python ids_simulation.py


### 🧪 For Real Packet Capture

- Run as administrator / root
- Install `scapy`
- Select appropriate network interface from UI settings

---

## 🧠 Model Training

- **Initial training** uses generated data
- **Custom data import**: Upload CSV via UI with these columns:
  - `Protocol`, `Port`, `Size`, `Attack` (0 = normal, 1 = attack)

---

## 💣 Simulated Attack Types

| Attack Type         | Characteristics                     |
|---------------------|--------------------------------------|
| Port Scanning       | Rapid SYN packets to multiple ports |
| DDoS                | High volume, same dest, large size  |
| Lateral Movement    | Internal IP communication patterns  |
| Amplification       | Small request → Large response (e.g., NTP, DNS) |

---

## 📈 User Interface Guide

- **Dashboard**: System status and alerts
- **Visualization Tab**: Real-time packet activity
- **Event Logs**: Full event details (IP, protocol, port, decision)
- **Statistics**: Model metrics, time series plots
- **Settings**: Toggle models, import data, adjust sensitivity

---

## ⚙️ Configuration Options

- Enable/disable detection models
- Adjust model sensitivity thresholds
- Set simulation speed (100ms–2000ms)
- Export logs / import training data

---

## 📤 Export & Integration

- Export all events as CSV logs
- Integrate with external tools via API or scripting
- SIEM, firewall, or notification extensions possible

---

## 🧩 Extending the System

- ➕ Add new detection models via `IDSModels.py`
- 📊 Add new visualizations using `PyQtGraph`
- 🌐 Connect to external systems (email, SIEM, firewalls)

---

## 🛠️ Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| No packets in real mode | No permission | Run as root or admin |
| High CPU | Too many events or fast speed | Slow simulation or clear data |
| Model inaccuracy | Poor training data | Import better CSV, adjust thresholds |

---

## 📋 License

This project is open-source and free to use for educational and research purposes.

---

## 🙌 Acknowledgements

Developed as part of an IoT Network Security System. Inspired by real-world threat models and designed for practical awareness, training, and experimentation. 

---

## 📎 Related Links

- 📘 [Project Documentation (PDF)](./documentation/IoT_IDS.pdf)
- 📊 [UNSW-NB15 Dataset](https://www.unsw.adfa.edu.au/unsw-canberra-cyber/cybersecurity/ADFA-NB15-Datasets/)


---
