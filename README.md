# CSI_6_SIT-DASH-Video-Streaming-Coursework
This project implements a DASH-based video streaming system using open-source tools and evaluates the impact of different network artefacts on Quality of Experience (QoE). The system was built using a Kali Linux server VM and an Ubuntu client VM connected through an internal VirtualBox network.
Objectives
- Install and configure FFmpeg for video transcoding
- Prepare two HD videos for adaptive streaming
- Generate DASH manifests and media segments
- Host DASH content on an Apache web server
- Play the stream using a dash.js-compatible player
- Simulate network artefacts using Linux traffic control
- Evaluate performance using Mean Opinion Score (MOS)
Tools Used
- Oracle VirtualBox
- Kali Linux
- Ubuntu
- FFmpeg
- Apache2
- dash.js
- tc (Linux Traffic Control)
- IPERF
- 
Video Preparation

Two HD videos were downloaded from Pexels and Videezy and transcoded into:

1.5 Mbps
2.0 Mbps
4.0 Mbps
DASH Packaging

FFmpeg was used to generate MPD manifests and segment files for adaptive streaming.

Web Server Setup

Apache2 was configured on the Kali Linux server to host the MPD and media segments.

Player Setup

The dash.js reference player was used on the Ubuntu client to play the DASH stream.

Network Configuration

The VMs were connected using a VirtualBox Internal Network to ensure traffic passed through the virtual interfaces and could be shaped correctly.

Traffic Control Scenarios
Scenario A – TBF
Rate: 2.5 Mbps
Burst: 20 KB
Latency: 50 ms
Scenario B – HTB
Guaranteed rate: 2.5 Mbps
Ceiling: 5 Mbps
Burst: 20 KB
IPERF traffic prioritised over video
Scenario C – Traffic Policing
Ingress limit: 3.5 Mbps
Excess traffic dropped
IPERF Testing

A 1 Mbps TCP IPERF connection was established between the client and server to simulate competing traffic.
