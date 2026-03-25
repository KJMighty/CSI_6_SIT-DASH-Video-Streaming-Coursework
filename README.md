# CSI_6_SIT-DASH-Video-Streaming-Coursework

## Module: Smart Internet Technologies (CSI_6_SIT)

This project implements a DASH-based video streaming system using open-source tools and evaluates the impact of different network artefacts on Quality of Experience (QoE). The system was built using a Kali Linux server VM and an Ubuntu client VM connected through an internal VirtualBox network.

---

## Objectives

- Install and configure FFmpeg for video transcoding  
- Prepare two HD videos for adaptive streaming  
- Generate DASH manifests and media segments  
- Host DASH content on an Apache web server  
- Play the stream using a dash.js-compatible player  
- Simulate network artefacts using Linux traffic control  
- Evaluate performance using Mean Opinion Score (MOS)  

---

## Tools Used

- Oracle VirtualBox  
- Kali Linux  
- Ubuntu  
- FFmpeg (video processing tool)  
- Apache2 (web server)  
- dash.js (DASH player)  
- tc (Linux Traffic Control)  
- IPERF (network testing tool)  

---

## Video Preparation

The videos were transcoded into the following bitrate representations:

- 1.5 Mbps  
- 2.0 Mbps  
- 4.0 Mbps  

Author
Kai Mighty 
Student ID: 4217377 
## Results Summary 
| Scenario | Condition | QoE Observation | MOS | |--------|----------|----------------|-----| | TBF | 2.5 Mbps | Moderate buffering, reduced quality | 3 | | HTB | 2.5–5 Mbps | Smooth playback, stable quality | 4 | | Policing | Packet loss (3.5 Mbps) | Stuttering, unstable playback | 2 |
