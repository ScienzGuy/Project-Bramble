# 🪐 Project Jupiter: A Hardened 4-Pi 5 Computing Ecosystem

**Project Jupiter** is a distributed high-performance computing (HPC) environment built on a cluster of four Raspberry Pi 5 nodes. The project's mission is to maximize computational efficiency, stability, and security for two distinct workloads: **Astrophysical/Mathematical Modeling** and **Local LLM Inference**.

## 🏗️ The Architecture: "The Tidy Pivot"
Originally designed as a containerized Nomad/Docker orchestration environment, the project underwent a significant architectural shift in January 2026. To eliminate the 5–10% virtualization overhead and close security vulnerabilities inherent in project-led container runpoints, the entire cluster was migrated to **Hardened Bare Metal**.

### 🌡️ Thermal & Mechanical Engineering
* **Subterranean Deployment:** Relocated to a subterranean basement environment to exploit a lower ambient thermal floor, maintaining a steady **49°C** under 100% sustained load.
* **Clock Optimization:** Pinned at **2200MHz** (the Pi 5 efficiency "sweet spot") with a custom undervolt delta to ensure silicon longevity.
* **CPU Governor:** Systemd-forced `performance` mode to eliminate frequency scaling latency.

* ## 🌌 Sub-Cluster A: Theia (Nodes: Ganymede & Callisto)
**Role:** Big Science & Discrete Mathematics  
**Compute Engine:** BOINC (Berkeley Open Infrastructure for Network Computing)

Theia is optimized for high-FPU throughput and utilizes the **asimd** (Advanced SIMD/NEON) and **asimddp** (Dot Product) instruction sets of the Cortex-A76 for accelerated vector math.

### 🧬 Science Portfolio & Resource Weighting
We utilize a weighted resource share to ensure the most critical astrophysical research receives the majority of CPU cycles.

| Project | Resource Share | Focus Area |
| :--- | :--- | :--- |
| **Einstein@home** | 100 | Gravitational Waves & Pulsar detection |
| **Rosetta@home** | 100 | Molecular Biology & Protein Folding |
| **PrimeGrid** | 50 | Mathematics (GFN-16 / GFN-17 searches) |
| **Asteroids@home** | 25 | Solar System Asteroid Shape Modeling |
| **Universe@Home** | 10 | Galactic Evolution & Black Hole Research |

## 🧠 Sub-Cluster B: GAIa (Nodes: Io & Europa)
**Role:** Generative Artificial Intelligence & Local Inference  
**Compute Engine:** Ollama / Open WebUI

GAIa provides local, private AI inference services. While the primary cluster is bare metal, GAIa utilizes a minimal Docker footprint for the Open WebUI frontend to maintain a clean interface for the family.

### 🛠️ Optimization Specs
* **Inference Engine:** Optimized for 8GB RAM footprints using 4-bit and 8-bit quantization.
* **Privacy Hardening:** All model weights and chat histories are stored locally; zero data egress to external LLM providers.

## 🛡️ Network & Security Hardening
* **Congestion Control:** Enabled **BBR (Bottleneck Bandwidth and RTT)** across all nodes to optimize large workunit transfers and model downloads.
* **RPC Lockdown:** Remote access restricted via `remote_hosts.cfg`; unauthorized subnet CIDR ranges are strictly prohibited.
* **Firewall:** Localized software firewall on each node, exposing only essential ports (BOINC RPC: 31416, SSH, WebUI).

## 📈 Monitoring & Maintenance
* **Live Stats:** Individual nodes monitored via **Glances** (Standalone mode).
* **Logs:** Filtered for architecture compatibility (`aarch64-unknown-linux-gnu`) to ensure zero "ghost" CPU cycles.
* **Vector Math Optimization:** Verified `asimd` and `asimddp` support; BOINC binaries utilizing Advanced SIMD (NEON) for Einstein@Home and PrimeGrid GFN workloads.

---
*Note: Theia shares the Project Jupiter chassis with the GAIa sub-cluster. This documentation covers the BOINC-specific implementation.*

**Maintained by Scienz_Guy | 2026**
