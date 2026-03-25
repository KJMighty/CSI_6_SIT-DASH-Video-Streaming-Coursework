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

### Example FFmpeg Commands

```bash
ffmpeg -i input.mp4 -b:v 1500k output_1.5.mp4
ffmpeg -i input.mp4 -b:v 2000k output_2.mp4
ffmpeg -i input.mp4 -b:v 4000k output_4.mp4
