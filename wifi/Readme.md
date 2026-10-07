# WIFI-PHYSX PRO LAB: Wi-Fi Signal & Network Interactive Simulator

An interactive, zero-dependency browser-based physics laboratory and protocol simulator for exploring RF wave propagation, Wi-Fi 7 (802.11be) architectures, channel spectrum allocation, CSMA/CA contention mechanisms, and network security protocols.

---

## 🌟 Key Modules

### 1. 📡 RF Floorplan & Signal Attenuation Engine
- **Real-Time Physics Canvas**: Renders continuous 2D radio wave fronts, ray paths, and dynamic RSSI heatmaps.
- **Friis Path Loss & Log-Distance Attenuation**: Dynamically calculates Free-Space Path Loss ($FSPL$) and signal degradation based on distance and carrier frequency:
  $$FSPL(\text{dB}) = 20\log_{10}(d) + 20\log_{10}(f) - 27.55$$
  *(where $d$ is distance in meters and $f$ is frequency in MHz).*
- **Material Obstacle Attenuation**: Placeable, draggable obstacles with real-world empirical absorption indices:
  - **Concrete Wall**: $-12\text{ dB}$
  - **Drywall / Stud**: $-3\text{ dB}$
  - **Glass Window**: $-2\text{ dB}$
  - **Metal Reinforced Barrier**: $-20\text{ dB}$
  - **Water Reservoir**: $-8\text{ dB}$
- **Phased Array Beamforming**: Interactive constructive interference modeling between multiple transmit antennas.
- **Multi-Hop Mesh Backhaul & 802.11r Roaming**: Drag client devices across the floorplan to trigger dynamic BSS transition and fast-reassociation handshakes between main and mesh nodes.

---

### 2. 🛰️ Live Network Inspector & Airspace Scanner
- **Host Hardware Telemetry**: Queries the `Network Information API` (`navigator.connection`) in real time for link downlink limits, round-trip time (RTT), and data-saver parameters.
- **WebRTC Subnet Discovery**: Probes local ICE candidate endpoints to identify client LAN subnet topology without administrative privileges.
- **Live Latency & Jitter Monitor**: Real-time packet round-trip benchmark plotting sequential ping variance and jitter on an active HTML5 Canvas.
- **Airspace 802.11 Beacon Scanner**: Simulates multi-band channel discovery (2.4 GHz, 5.0 GHz, and 6.0 GHz) with dynamic signal fluctuations, BSSID inspection, and channel width evaluation.
- **One-Click Simulator Synchronization**: Syncs detected host metrics (frequency band, channel width, and estimated link budget) directly into the interactive floorplan simulator.
- **Custom SSID Injection**: Allows manual entry of local networks to test channel overlaps and coexistence.

---

### 3. ⚡ Wi-Fi 7 (802.11be) Deep-Dive
- **4096-QAM Interactive Constellation Map**: Renders a live $64 \times 64$ symbol constellation diagram carrying 12 bits per symbol, paired with Error Vector Magnitude (EVM) target gauges.
- **Multi-Link Operation (MLO)**: Interactive toggle demonstrating Simultaneous Transmit and Receive (STR mode) across 2.4 GHz, 5 GHz, and 6 GHz bands to minimize airtime latency.
- **Preamble Puncturing & Ultra-Wide 320 MHz Channels**: Visual breakdown of spectrum slicing that preserves channel throughput even when sub-bands experience localized radar or legacy interference.

---

### 4. 📊 Spectrum Highway & Channel Bonding
- **OFDMA Resource Units (RUs)**: Visual comparison of subcarrier tone partitioning ($26$, $52$, and $106$-tone RUs) versus traditional single-carrier multiplexing.
- **MU-MIMO Spatial Stream Visualizer**: Real-time rendering of multi-antenna beam steering separating multiple client links simultaneously over the same frequency channel.

---

### 5. 🔄 CSMA/CA Protocol State Machine
- **Listen-Before-Talk (LBT) Engine**: Interactive 5-phase timeline modeling:
  1. **DIFS / Carrier Sense**: Energy detection before transmission attempt.
  2. **Contention Window & Random Backoff Slot**: Collision avoidance wait timers.
  3. **RTS / CTS Handshake**: Request-to-Send and Clear-to-Send channel reservation frames.
  4. **Payload Frame Airtime**: High-throughput physical transmission slot.
  5. **Block ACK**: Positive acknowledgement reception.
- **Collision Simulator**: Trigger mid-air contention conflicts to observe exponential backoff window doubling ($CW_{min} \rightarrow CW_{max}$).

---

### 6. 🛡️ Security & Encryption Sandbox
- **WEP (Legacy)**: Explains 24-bit weak IV vulnerabilities and RC4 keystream reuse.
- **WPA2-Personal (AES-CCMP)**: Explores 4-Way Handshake mechanics and vulnerability to offline dictionary attacks via $WPA$ capture frames.
- **WPA3-SAE (Dragonfly)**: Simulates Elliptic Curve Simultaneous Authentication of Equals zero-knowledge proofs and Protected Management Frames ($802.11w$).
- **Evil Twin / Rogue AP Alert**: Simulates detection of rogue spoofed BSSID transmitters.

---

### 7. 🩺 Network Doctor & Diagnostic Auditor
- **Coverage Index**: Calculates floorplan SNR budgets, airtime balance, and mesh node geometry.
- **Actionable Optimization Advice**: Generates automated recommendations for channel widths, antenna placement, and DFS channel selection.
- **Printable Audit Report**: Formatted CSS print stylesheets for exporting one-click diagnostic assessments.

---

## 📁 Repository Structure

```
├── index.html                           # Single-file standalone simulator & application
├── README.md                            # Project documentation
├── wan_network_detection_explained.md   # Architectural guide: LAN vs WAN boundaries & browser sandboxing
└── desktop_app_network_access.md        # Technical guide: OS APIs & UPnP/SNMP native implementations
```

---

## 🚀 Getting Started

The core application runs completely client-side with no backend server, npm dependencies, or build tools required.

### Run Directly in Browser
1. Clone or download the repository.
2. Open `index.html` in any modern web browser (Google Chrome, Mozilla Firefox, Microsoft Edge, or Apple Safari):
   ```bash
   # Linux / macOS
   open index.html
   
   # Windows PowerShell
   Start-Process index.html
   ```

### Run via Lightweight Local Server (Optional)
To test WebRTC ICE candidate probing without local file scheme restrictions:
```bash
# Python 3
python -m http.server 8080

# Node.js
npx serve .
```
Navigate to `http://localhost:8080` in your browser.

---

## 🧮 Mathematical & Attenuation Models

The simulation engine calculates received signal power $P_{rx}$ at any coordinate using the following composite formula:

$$P_{rx} = P_{tx} + G_{tx} + G_{rx} - FSPL(d, f) - \sum_{i=1}^{n} L_{\text{obstacle}, i}$$

Where:
- $P_{tx}$: Transmitter power in dBm (configurable between $5\text{ dBm}$ and $30\text{ dBm}$).
- $G_{tx}, G_{rx}$: Antenna gain factors ($+3\text{ dBi}$ with beamforming active).
- $FSPL(d, f)$: Free-Space Path Loss across distance $d$ (meters) and frequency $f$ (MHz).
- $L_{\text{obstacle}, i}$: Specific attenuation in dB for each intersected wall or physical barrier along the line-of-sight ray vector.
- $\text{Noise Floor}$: Defaulted to $-95\text{ dBm}$ thermal noise in typical residential environments.
- $\text{SNR (Signal-to-Noise Ratio)}$: $P_{rx} - \text{Noise Floor}$.

---

## 🔒 Security & Privacy Notice

This software is designed strictly for educational, design, and diagnostic purposes. The Live Network Inspector relies exclusively on public, standard browser interfaces (`navigator.connection` and local WebRTC STUN candidate discovery). It does not conduct unauthorized airspace sniffing or transmit network credentials to any remote server.

---

## 📄 License

Distributed under the MIT License. Open source and free for educational and research use.