# Wi-Fi 6 System-Level Simulator in MATLAB

## 📡 Project Overview
[cite_start]This project presents the implementation and analysis of a system-level simulation for WLAN networks based on the IEEE 802.11ax (Wi-Fi 6) standard[cite: 71]. [cite_start]Built entirely in MATLAB, this application features a custom Graphical User Interface (GUI) to configure a multi-node network (Access Point and Stations)[cite: 72]. 

[cite_start]Instead of computationally expensive bit-by-bit physical layer simulations, this project uses **PHY abstraction** (Link-to-System modeling)[cite: 115]. [cite_start]It approximates network performance mathematically based on node distance, allowing for rapid evaluation of Throughput, Packet Loss Ratio (PER), and Latency[cite: 72, 129, 140].

![GUI Configuration Tab](images/config-tab.jpg) ## ⚙️ Features & Architecture
[cite_start]The MATLAB GUI is divided into three functional tabs[cite: 3, 4]:

### 1. Topology & Configuration
* [cite_start]Allows users to define the (X, Y) coordinates for one Access Point (AP) and two Stations (STA1, STA2) on a 2D grid[cite: 7, 8, 9, 10, 11].
* [cite_start]Includes settings for simulation time and PHY/MAC abstraction methods[cite: 12, 13, 14].

### 2. MAC Layer Traffic Visualization (Gantt Chart)
[cite_start]To visualize the Media Access Control (MAC) sublayer, the simulator generates a probabilistic Gantt chart representing the **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) mechanism[cite: 119, 172].

[cite_start]The node states are dynamically generated based on calculated packet loss and defined probabilities[cite: 173]:
* [cite_start]**Transmission (Green):** The node actively transmits data (PPDU)[cite: 148, 188]. [cite_start]The AP has a higher transmission bias than the stations[cite: 174].
* [cite_start]**Idle (White):** The node has no data to transmit and the channel is free[cite: 143, 189].
* [cite_start]**Contention (Yellow):** Represents the random backoff period where the node waits to avoid collisions[cite: 147, 190].
* [cite_start]**Reception (Blue):** Successful reception of a packet destined specifically to that node[cite: 150, 191].
* [cite_start]**Overhearing (Cream):** The node detects the medium is occupied by a transmission not addressed to it, postponing its own transmission[cite: 152, 192].
* [cite_start]**Failure (Red):** Represents a corrupted message or packet loss, which increases proportionally with distance[cite: 153, 175, 193].

### 3. Performance Metrics
[cite_start]Calculates and displays performance bar charts based on the Euclidean distance ($d$) between the AP and each station[cite: 163, 221]:
* [cite_start]**Throughput:** Modeled as an exponential decay based on distance: $Th = 10 \cdot e^{-d/70}$[cite: 164, 166, 167].
* [cite_start]**Packet Loss Ratio:** Threshold logic where losses are $0$ up to $50m$, then increase linearly using $(d-50)/40$[cite: 169].
* [cite_start]**Latency:** Calculated as a base value of $0.2s$ plus a distance-dependent component ($d/500$)[cite: 170].

![Performance Metrics Tab](images/performance-tab.jpg) ## 🚀 How to Run
1. Open MATLAB.
2. Run the `CodFinalProiect.m` script.
3. Use the **Configuration & Topology** tab to move the AP and Stations.
4. [cite_start]Click **RUN SIMULATION** to generate the traffic Gantt chart and view the calculated metrics[cite: 16, 161].
