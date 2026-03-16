# Wi-Fi 6 System-Level Simulator in MATLAB

## 📡 Project Overview
This project presents the implementation and analysis of a system-level simulation for WLAN networks based on the IEEE 802.11ax (Wi-Fi 6) standard. Built entirely in MATLAB, this application features a custom Graphical User Interface (GUI) to configure a multi-node network (Access Point and Stations). 

Instead of computationally expensive bit-by-bit physical layer simulations, this project uses **PHY abstraction** (Link-to-System modeling). It approximates network performance mathematically based on node distance, allowing for rapid evaluation of Throughput, Packet Loss Ratio (PER), and Latency.

![GUI Configuration Tab](images/config-tab.jpg)

## ⚙️ Features & Architecture
The MATLAB GUI is divided into three functional areas:

### 1. Topology & Configuration
* Allows users to define the (X, Y) coordinates for one Access Point (AP) and two Stations (STA1, STA2) on a 2D grid.
* Provides inputs for simulation time and allows toggling PHY/MAC abstraction methods.

### 2. MAC Layer Traffic Visualization (Gantt Chart)
To visualize the Media Access Control (MAC) sublayer, the simulator generates a probabilistic Gantt chart representing the **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) mechanism. The node states are dynamically generated based on calculated packet loss and defined probabilities:
* **Transmission (Green):** The node actively transmits data (PPDU). The AP has a higher transmission bias than the stations.
* **Idle (White):** The node has no data to transmit and the channel is free.
* **Contention (Yellow):** Represents the random backoff period where the node waits to avoid collisions.
* **Reception (Blue):** Successful reception of a packet destined specifically to that node.
* **Overhearing (Cream):** The node detects the medium is occupied by a transmission not addressed to it, postponing its own transmission.
* **Failure (Red):** Represents a corrupted message or packet loss, which increases proportionally with distance.

### 3. Performance Metrics
The system calculates and displays performance bar charts based on the Euclidean distance ($d$) between the AP and each station:
* **Throughput:** Modeled as an exponential decay based on distance: $Th = 10 \cdot e^{-d/70}$.
* **Packet Loss Ratio:** Uses threshold logic where losses are $0$ up to $50m$, then increase linearly.
* **Latency:** Calculated as a base value of $0.2s$ plus a distance-dependent component ($d/500$).

![Performance Metrics Tab](images/performance-tab.jpg)

## 🔬 Methodology & Simulation Accuracy
This simulator is designed around the principles of the **IEEE 802.11 TGax evaluation methodology**. By abstracting the Physical Layer, the system maps the Signal-to-Interference-plus-Noise Ratio (SINR) directly to Packet Error Rate (PER) curves. 

This Link-to-System (L2S) approach ensures that the macroscopic behavior of the network (throughput degradation over distance, increased collisions, and latency spikes) is modeled accurately without the massive computational overhead required by full waveform modeling. The probabilistic state machine effectively demonstrates the time-sharing nature of dense Wi-Fi 6 deployments.
