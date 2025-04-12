# IoT IDS Simulation System

## Table of Contents

1. [Introduction](#1-introduction)
   - [Overview](#11-overview)
   - [Purpose and Goals](#12-purpose-and-goals)
   - [System Architecture](#13-system-architecture)

2. [Core Components](#2-core-components)
   - [PacketCapture](#21-packetcapture)
   - [IDSModels](#22-idsmodels)
   - [SimulationWindow](#23-simulationwindow)
   - [NotificationSystem](#24-notificationsystem)

3. [Detection Methods](#3-detection-methods)
   - [Signature-based Detection](#31-signature-based-detection)
   - [Anomaly-based Detection](#32-anomaly-based-detection)
   - [Deep Learning Detection](#33-deep-learning-detection)
   - [Ensemble Decision Making](#34-ensemble-decision-making)

4. [User Interface Guide](#4-user-interface-guide)
   - [Dashboard Overview](#41-dashboard-overview)
   - [Visualization Tab](#42-visualization-tab)
   - [Event Logs Tab](#43-event-logs-tab)
   - [Statistics Tab](#44-statistics-tab)
   - [Settings Tab](#45-settings-tab)
   - [Control Panel](#46-control-panel)

5. [Data Flow](#5-data-flow)
   - [Packet Acquisition](#51-packet-acquisition)
   - [Feature Extraction](#52-feature-extraction)
   - [Analysis Pipeline](#53-analysis-pipeline)
   - [Visualization Process](#54-visualization-process)

6. [Model Training](#6-model-training)
   - [Initial Training](#61-initial-training)
   - [Importing Custom Training Data](#62-importing-custom-training-data)
   - [Model Evaluation](#63-model-evaluation)

7. [System Configuration](#7-system-configuration)
   - [Network Interface Selection](#71-network-interface-selection)
   - [Model Sensitivity Settings](#72-model-sensitivity-settings)
   - [Simulation Speed](#73-simulation-speed)

8. [Alert System](#8-alert-system)
   - [Alert Thresholds](#81-alert-thresholds)
   - [Notification Types](#82-notification-types)
   - [Alert Responses](#83-alert-responses)

9. [Data Management](#9-data-management)
   - [Exporting Logs](#91-exporting-logs)
   - [Importing Data](#92-importing-data)
   - [Data Retention](#93-data-retention)

10. [Attack Types](#10-attack-types)
    - [Port Scanning](#101-port-scanning)
    - [DDoS Attacks](#102-ddos-attacks)
    - [Lateral Movement](#103-lateral-movement)
    - [Amplification Attacks](#104-amplification-attacks)

11. [Extension Guide](#11-extension-guide)
    - [Adding New Detection Models](#111-adding-new-detection-models)
    - [Implementing New Visualizations](#112-implementing-new-visualizations)
    - [Integration with External Systems](#113-integration-with-external-systems)

12. [Troubleshooting](#12-troubleshooting)
    - [Common Issues](#121-common-issues)
    - [Performance Considerations](#122-performance-considerations)
    - [Debugging Tips](#123-debugging-tips)

13. [Requirements and Dependencies](#13-requirements-and-dependencies)
    - [Software Dependencies](#131-software-dependencies)
    - [Hardware Requirements](#132-hardware-requirements)
    - [Installation Guide](#133-installation-guide)

---

## 1. Introduction

### 1.1 Overview

The Advanced IoT IDS (Intrusion Detection System) Simulation is a comprehensive platform designed to detect, analyze, and visualize network security threats in real-time. It combines multiple detection methodologies with an intuitive interface to provide both educational insights and practical security monitoring.

This system simulates network traffic patterns and applies various detection algorithms to identify potential security threats, making it suitable for education, research, and security awareness training.

### 1.2 Purpose and Goals

The system serves several key purposes:

- **Educational Tool**: Demonstrate how different IDS detection methods work
- **Research Platform**: Allow experimentation with different detection algorithms
- **Security Awareness**: Visualize attack patterns and normal network behavior
- **Testing Environment**: Provide a safe environment to simulate cyber attacks and their detection

Primary goals include:
- Real-time visualization of network traffic patterns
- Implementation of multiple detection methodologies
- Detailed logging and analysis of network events
- Customizable simulation parameters
- Support for both simulated and real network traffic

### 1.3 System Architecture

The system follows a modular architecture with four primary components:

1. **Data Acquisition Layer**: Responsible for gathering network packets either through simulation or real network capture
2. **Analysis Layer**: Contains the detection models that identify potential threats
3. **Visualization Layer**: Presents the data in an intuitive graphical interface
4. **Notification Layer**: Manages alerts and responses to detected threats

These components interact in a pipeline, where network packets flow through the system, are analyzed by detection models, and results are displayed to the user.

```
[Data Acquisition] → [Feature Extraction] → [Detection Models] → [Decision Engine]
                                                                       ↓
[Notification System] ← [Alert Generation] ← [Results Aggregation] ← [Decision Engine]
        ↓
[User Interface] → [Visualization] → [Logs] → [Statistics]
```

## 2. Core Components

### 2.1 PacketCapture

The `PacketCapture` class handles all aspects of network data acquisition, whether simulated or real.

#### Key Features:
- Support for both simulated and real network packet capture
- Feature extraction from raw packets
- Realistic pattern generation for various network protocols
- Configurable attack simulation with adjustable parameters
- Buffer management for packet history

#### Methods:
- `get_next_packet()`: Retrieves the next packet from the network or simulation
- `get_feature_vector()`: Extracts numerical features from a packet for model input
- `_generate_sample_packet()`: Creates a realistic simulated packet
- `_extract_features()`: Processes a real packet to extract relevant features

#### Usage Example:
```python
# Initialize packet capture with simulation mode
packet_capture = PacketCapture(use_sample_data=True)

# Get next packet
packet = packet_capture.get_next_packet()

# Extract feature vector for model input
feature_vector = packet_capture.get_feature_vector(packet)
```

### 2.2 IDSModels

The `IDSModels` class encapsulates all detection algorithms and their parameters.

#### Key Features:
- Multiple detection methodologies in a single interface
- Signature-based detection using classifier models
- Anomaly-based detection using unsupervised learning
- Deep learning detection placeholders
- Voting mechanisms for ensemble decisions

#### Methods:
- `predict(feature_vector)`: Runs all detection models and returns combined results
- `_initialize_models()`: Sets up initial model training with sample data

#### Usage Example:
```python
# Initialize detection models
ids_models = IDSModels()

# Make predictions on a feature vector
predictions = ids_models.predict(feature_vector)

# Access individual model decisions
signature_result = predictions['signature']
anomaly_result = predictions['anomaly']
final_decision = predictions['final']
```

### 2.3 SimulationWindow

The `SimulationWindow` class is the main UI component that manages the entire application.

#### Key Features:
- Tabbed interface for different views (visualization, logs, statistics, settings)
- Real-time data visualization using PyQtGraph
- Event logging and tabular display
- Control panel for simulation parameters
- Configuration options for detection models

#### Key Methods:
- `update_simulation()`: Main simulation loop that processes events
- `_update_visualizations()`: Updates all visual elements with new data
- `export_logs()`: Exports event data to CSV
- `import_training_data()`: Imports external data for model training

### 2.4 NotificationSystem

The `NotificationSystem` class handles alert generation and notification delivery.

#### Key Features:
- Threshold-based alerting for different attack types
- Alert logging and history
- Visual notifications through the UI
- Extensible for external notification mechanisms (email, SIEM)

#### Methods:
- `process_event(event)`: Analyzes an event and triggers alerts if needed
- `_send_notification(attack_type, event)`: Delivers notifications through configured channels

## 3. Detection Methods

### 3.1 Signature-based Detection

Signature-based detection identifies known attack patterns by comparing network traffic against a database of signatures.

#### Implementation:
- Uses a RandomForestClassifier from scikit-learn
- Features include protocol, port, and packet size
- Model is trained on labeled examples of normal and attack traffic
- Returns binary classification (0 = normal, 1 = attack)

#### Advantages:
- High precision for known attacks
- Low false positive rate
- Fast detection speed

#### Limitations:
- Cannot detect novel or zero-day attacks
- Requires regular signature updates
- Pattern variations may evade detection

### 3.2 Anomaly-based Detection

Anomaly detection identifies traffic that deviates significantly from normal behavior.

#### Implementation:
- Uses an IsolationForest algorithm
- Trained on normal traffic only
- Evaluates new traffic based on its deviation from the norm
- Returns anomaly score converted to binary decision

#### Advantages:
- Can detect novel and zero-day attacks
- Does not require known attack signatures
- Adaptable to changing network environments

#### Limitations:
- Higher false positive rate
- Requires accurate baseline of normal behavior
- Performance depends on training data quality

### 3.3 Deep Learning Detection

The deep learning component is a placeholder for more sophisticated neural network-based detection.

#### Planned Implementation:
- Will use CNN or RNN models for sequential pattern recognition
- Feature extraction from packet sequences
- Capability to detect complex attack patterns
- Returns probability of attack

#### Current Simulation:
- Uses a probability influenced by other model decisions
- Simulates correlation between detection methods

### 3.4 Ensemble Decision Making

The final decision combines results from all detection methods using a voting mechanism.

#### Implementation:
- Simple majority voting (2 out of 3 models indicating attack)
- Each model has equal weight in the current implementation
- Extensible for weighted voting

#### Advantages:
- Combines strengths of multiple detection methods
- Reduces false positives from individual models
- More robust than any single detection method

## 4. User Interface Guide

### 4.1 Dashboard Overview

The dashboard provides at-a-glance system status and key metrics.

#### Components:
- **Status Indicator**: Shows if monitoring is active or stopped
- **Packet Counter**: Displays total packets processed
- **Alert Counter**: Shows number of detected attacks
- **Last Alert**: Details of the most recent security alert

### 4.2 Visualization Tab

The visualization tab provides a graphical representation of network traffic.

#### Components:
- **Scatter Plot**: Displays events with port (x-axis) vs. packet size (y-axis)
- **Color Coding**: Green for normal traffic, red for detected attacks
- **Interactive Elements**: Click an event for detailed information
- **Legend**: Identifies plot elements

#### Interaction:
To view details of a specific event:
1. Click on any point in the scatter plot
2. A popup will display detailed information about the selected event
3. Information includes all detection results and packet metadata

### 4.3 Event Logs Tab

The event logs tab provides detailed textual information about each event.

#### Components:
- **Text Log**: Chronological list of all events with basic details
- **Event Table**: Structured view with columns for all event properties
- **Color Coding**: Attack events highlighted in red

#### Table Columns:
- Time
- Event ID
- Source IP
- Destination IP
- Protocol
- Port
- Decision (Normal/Attack)

### 4.4 Statistics Tab

The statistics tab provides analytical data about traffic patterns and detection results.

#### Components:
- **Time Series Plot**: Shows attack trends over time
- **Attack Type Distribution**: Bar chart of different attack categories
- **Model Performance Metrics**: Statistics on true/false positives per model

### 4.5 Settings Tab

The settings tab allows configuration of various system parameters.

#### Components:
- **Network Interface Selection**: Choose between simulated or real network data
- **Model Settings**: Enable/disable individual detection models
- **Sensitivity Sliders**: Adjust threshold parameters for each model
- **Data Management**: Export logs and import training data

### 4.6 Control Panel

The control panel provides global controls for the simulation.

#### Components:
- **Start Button**: Begins the simulation/monitoring
- **Stop Button**: Pauses the simulation/monitoring
- **Speed Slider**: Controls the update frequency
- **Clear Button**: Resets all data and visualizations

## 5. Data Flow

### 5.1 Packet Acquisition

The packet acquisition process determines how network packets enter the system.

#### Simulated Mode:
1. System generates realistic packet metadata based on predefined patterns
2. Normal and attack traffic are generated with configurable probabilities
3. Packet features include realistic network attributes (IP, protocol, size, etc.)

#### Real Network Mode:
1. System uses Scapy to capture packets from a selected network interface
2. Raw packets are processed to extract relevant features
3. Captured packets are added to the processing pipeline

### 5.2 Feature Extraction

Feature extraction converts raw packet data into numerical vectors for model input.

#### Extracted Features:
- Protocol (encoded as number)
- Destination port
- Packet size
- (Extensible for additional features)

#### Process:
1. Raw packet or simulated data is passed to feature extraction
2. Categorical features are converted to numerical representations
3. Features are combined into a vector
4. Vector is formatted for model input

### 5.3 Analysis Pipeline

The analysis pipeline processes each packet through multiple detection models.

#### Steps:
1. Feature vector is passed to each enabled detection model
2. Each model returns its decision (normal/attack)
3. Ensemble mechanism combines individual decisions
4. Final decision and individual model results are stored with the event

### 5.4 Visualization Process

The visualization process converts detection results into graphical representations.

#### Steps:
1. New events are added to the event history
2. Visualization components extract relevant data (e.g., port, size, decision)
3. Graphical elements are updated with new data points
4. Colors and styles are applied based on detection results
5. Statistics are recalculated for time series and distribution charts

## 6. Model Training

### 6.1 Initial Training

The system initializes with pre-trained models using generated sample data.

#### Process:
1. Sample data is generated with a mix of normal and attack patterns
2. Data is split into feature vectors and labels
3. Signature model is trained on all data
4. Anomaly model is trained only on normal traffic
5. Models are ready for prediction upon system startup

### 6.2 Importing Custom Training Data

Users can import their own training data to customize the detection models.

#### Requirements:
- CSV file with required columns: Protocol, Port, Size, Attack
- Attack column should contain binary values (0 = normal, 1 = attack)

#### Process:
1. User selects a CSV file via the Settings tab
2. System validates the file format
3. Data is loaded and processed
4. Models are retrained with the new data
5. System confirms successful training

### 6.3 Model Evaluation

The system tracks basic performance metrics for each model.

#### Metrics:
- True Positives: Correctly identified attacks
- False Positives: Normal traffic incorrectly flagged as attacks
- Accuracy: Overall correct classifications

#### Limitations:
- In simulation mode, ground truth is known
- In real network mode, feedback is required for accurate metrics

## 7. System Configuration

### 7.1 Network Interface Selection

Users can choose between simulated data or real network traffic.

#### Options:
- **Use Sample Data**: System generates realistic network traffic
- **Use Real Network Data**: System captures packets from a network interface

#### Interface Selection:
When using real network data, users can select the network interface to monitor from a dropdown list.

### 7.2 Model Sensitivity Settings

Users can adjust the sensitivity of each detection model.

#### Settings:
- **Signature Threshold**: Adjusts classification threshold for signature model
- **Anomaly Threshold**: Controls sensitivity to deviations from normal
- **Model Enable/Disable**: Toggles each model's participation in detection

#### Effects:
- Higher sensitivity increases detection rate but may increase false positives
- Lower sensitivity reduces false positives but may miss some attacks

### 7.3 Simulation Speed

Controls how quickly the system processes and displays new events.

#### Settings:
- Speed slider ranges from 100ms to 2000ms
- Lower values increase simulation speed
- Higher values slow down for easier observation

## 8. Alert System

### 8.1 Alert Thresholds

The system uses configurable thresholds to determine when to trigger alerts.

#### Default Thresholds:
- Port Scan: 3 events
- DDoS: 1 event (immediate alert)
- Lateral Movement: 2 events
- Amplification: 2 events
- Unknown attacks: 5 events

#### Threshold Logic:
- System counts events of each attack type
- When count reaches threshold, alert is triggered
- Counter resets after alert is triggered

### 8.2 Notification Types

The system supports multiple notification mechanisms.

#### Implemented:
- In-application alert dialogs
- Visual indicators on dashboard
- Event logging with highlighting

#### Extensible For:
- Email notifications
- SIEM integration
- Automated response triggers

### 8.3 Alert Responses

The system can be extended to respond automatically to detected threats.

#### Potential Responses:
- Logging detailed information
- Triggering external scripts
- Integrating with firewall APIs
- Executing predefined security playbooks

## 9. Data Management

### 9.1 Exporting Logs

Users can export event logs for external analysis.

#### Process:
1. Click "Export Logs" in the Settings tab
2. Select destination file location and name
3. System exports all events to CSV format
4. Confirmation dialog displays success status

#### Exported Data:
- All event metadata
- Detection results from each model
- Final decisions
- Timestamps and identifiers

### 9.2 Importing Data

Users can import external data for model training.

#### Process:
1. Click "Import Training Data" in the Settings tab
2. Select CSV file containing training data
3. System validates file format
4. Models are retrained with new data
5. Confirmation dialog displays results

### 9.3 Data Retention

The system manages event history with memory considerations.

#### Current Implementation:
- All events are stored in memory during the session
- Visualizations display limited recent history (last 100 events)
- Clear Data functionality removes all stored events

#### Considerations for Extension:
- Database integration for persistent storage
- Data rotation policies for long-running deployments
- Compression strategies for large datasets

## 10. Attack Types

### 10.1 Port Scanning

Port scanning involves probing a network host for open ports to identify vulnerable services.

#### Simulation Characteristics:
- Multiple connection attempts to different ports
- Small packet sizes
- TCP SYN flags
- Rapid connection sequence

#### Detection Methods:
- Signature-based: Pattern of multiple SYN packets to different ports
- Anomaly-based: Unusual connection patterns
- Visual: Appears as horizontal cluster in visualization

### 10.2 DDoS Attacks

Distributed Denial of Service attacks flood a target with excessive traffic.

#### Simulation Characteristics:
- High volume of packets
- Similar destination ports
- Large packet sizes
- Multiple source IPs

#### Detection Methods:
- Signature-based: Traffic volume exceeding thresholds
- Anomaly-based: Deviation from normal traffic patterns
- Visual: Appears as concentrated cluster in visualization

### 10.3 Lateral Movement

Lateral movement involves an attacker moving through a network after initial compromise.

#### Simulation Characteristics:
- Internal to internal communications
- Unusual service port access
- Access to management protocols

#### Detection Methods:
- Signature-based: Access to sensitive ports from unusual sources
- Anomaly-based: Deviation from normal internal traffic patterns
- Visual: Appears as unusual internal connection patterns

### 10.4 Amplification Attacks

Amplification attacks use protocols that return larger responses than requests for DDoS.

#### Simulation Characteristics:
- UDP protocol
- Specific service ports (DNS, NTP, SSDP)
- Small requests, large responses

#### Detection Methods:
- Signature-based: Known amplification protocol patterns
- Anomaly-based: Unusual response size ratios
- Visual: Appears as large packet sizes on specific ports

## 11. Extension Guide

### 11.1 Adding New Detection Models

The system architecture allows for integration of additional detection models.

#### Steps:
1. Create a new model class or instance
2. Add the model to the `IDSModels` class
3. Implement prediction method for the new model
4. Update the ensemble voting mechanism to include the new model
5. Add UI elements for model configuration

#### Example:
```python
# In IDSModels class
self.heuristic_model = CustomHeuristicModel()

# In predict method
heuristic_prediction = self.heuristic_model.detect(feature_vector)
predictions['heuristic'] = heuristic_prediction

# Update voting mechanism
votes = sig_prediction + anom_prediction + cnn_prediction + heuristic_prediction
final_decision = 1 if votes >= (len(predictions) // 2 + 1) else 0
```

### 11.2 Implementing New Visualizations

The UI architecture supports adding new visualization types.

#### Steps:
1. Create a new PyQtGraph widget
2. Add the widget to the appropriate tab
3. Implement update logic in `_update_visualizations()`
4. Connect any interactive elements

#### Example:
```python
# Create new visualization
self.flowGraph = pg.GraphItem()
self.plotWidget.addItem(self.flowGraph)

# Update logic
def update_flow_graph(self):
    # Extract graph structure from events
    pos, adj, symbols, colors = self._create_flow_data()
    self.flowGraph.setData(pos=pos, adj=adj, symbolBrush=colors)
```

### 11.3 Integration with External Systems

The system can be extended to interact with external security tools.

#### Integration Points:
- **SIEM Systems**: Export events to Security Information and Event Management systems
- **Firewall APIs**: Trigger rule updates based on detections
- **Threat Intelligence**: Query external databases for IP reputation
- **Email/SMS Alerts**: Send notifications to security teams

#### Implementation Example:
```python
def send_to_siem(self, event):
    """Send event to SIEM system via API"""
    import requests
    
    siem_url = "https://siem.example.com/api/events"
    payload = {
        "source": "IDS-Simulator",
        "severity": "high" if event['predictions']['final'] == 1 else "low",
        "event_type": event['attack_type'] or "traffic",
        "source_ip": event['src_ip'],
        "destination_ip": event['dst_ip'],
        "timestamp": event['time'],
        "details": event
    }
    
    try:
        response = requests.post(siem_url, json=payload)
        return response.status_code == 200
    except Exception as e:
        print(f"SIEM integration error: {e}")
        return False
```

## 12. Troubleshooting

### 12.1 Common Issues

#### Packet Capture Failures
- **Symptom**: No real packets captured when using real network mode
- **Possible Causes**:
  - Insufficient permissions to access network interface
  - Interface in incorrect mode
  - No traffic on selected interface
- **Resolution**:
  - Run application with administrator/root privileges
  - Verify interface exists and is enabled
  - Test with a known-active interface

#### High CPU Usage
- **Symptom**: Application consumes excessive CPU resources
- **Possible Causes**:
  - Update frequency set too high
  - Too many events in memory
  - Visualization rendering overhead
- **Resolution**:
  - Reduce update frequency (increase timer interval)
  - Clear data periodically
  - Limit visualization to fewer elements

#### Model Accuracy Issues
- **Symptom**: Poor detection results, many false positives/negatives
- **Possible Causes**:
  - Insufficient training data
  - Inappropriate feature selection
  - Model parameters not optimized
- **Resolution**:
  - Import more representative training data
  - Adjust model sensitivity settings
  - Implement more sophisticated feature extraction

### 12.2 Performance Considerations

#### Memory Management
- Event history can grow large during extended sessions
- Consider implementing data rotation or database storage for long runs
- Use deque with maxlen for visualization data to limit memory usage

#### Processing Efficiency
- Feature extraction is the most computationally intensive operation
- Consider batch processing for multiple packets
- Optimize visualization updates for large datasets

#### UI Responsiveness
- Use separate threads for packet processing and UI updates
- Implement rate limiting for visualization updates
- Consider asynchronous processing for real network capture

### 12.3 Debugging Tips

#### Logging
- Enable verbose logging for troubleshooting
- Add logging statements to key processing steps
- Capture raw packet data for verification

#### Visual Debugging
- Use the visualization to identify patterns and anomalies
- Compare model decisions to identify discrepancies
- Examine feature vectors for unusual values

#### Model Inspection
- Print model parameters and thresholds
- Visualize decision boundaries for classifier models
- Analyze feature importance for signature-based detection

## 13. Requirements and Dependencies

### 13.1 Software Dependencies

#### Python Libraries
- **PyQt5**: GUI framework
- **PyQtGraph**: Real-time plotting
- **scikit-learn**: Machine learning models
- **numpy**: Numerical computing
- **pandas**: Data manipulation
- **scapy**: Network packet manipulation (for real capture mode)

#### Version Requirements
- Python 3.6 or higher
- PyQt5 5.12 or higher
- scikit-learn 0.24 or higher
- numpy 1.19 or higher
- pandas 1.1 or higher
- scapy 2.4 or higher (optional for real capture)

### 13.2 Hardware Requirements

#### Minimum Requirements
- CPU: Dual-core 2GHz
- RAM: 4GB
- Storage: 100MB for application
- Network: Any compatible interface for real capture

#### Recommended Specifications
- CPU: Quad-core 3GHz
- RAM: 8GB or higher
- Storage: 1GB for application and logs
- Network: Gigabit Ethernet for high-volume capture

### 13.3 Installation Guide

#### Basic Installation
1. Install Python 3.6 or higher
2. Install required packages:
   ```
   pip install PyQt5 pyqtgraph scikit-learn numpy pandas
   ```
3. For real packet capture, install scapy:
   ```
   pip install scapy
   ```
4. Clone or download the application source code
5. Run the main application:
   ```
   python ids_simulation.py
   ```

#### Additional Setup for Real Capture
1. Ensure proper network interface permissions:
   - Windows: Run as Administrator
   - Linux: Run with sudo or add user to netdev group
   - macOS: Install libpcap and run with sudo

2. Configure firewall to allow packet capture

3. For production environments, consider creating a dedicated virtual environment:
   ```
   python -m venv ids_env
   source ids_env/bin/activate  # Linux/macOS
   ids_env\Scripts\activate     # Windows
   pip install -r requirements.txt
   ```
