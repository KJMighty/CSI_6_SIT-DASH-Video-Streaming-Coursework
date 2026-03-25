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
  
Video Preparation

The videos were transcoded into the following bitrate representations:

- 1.5 Mbps
- 2.0 Mbps
- 4.0 Mbps

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

Installation and Deployment Instructions
1. Install FFmpeg
- sudo apt update
- sudo apt install ffmpeg
2. Install Apache
- sudo apt install apache2
3. Transcode video
- ffmpeg -i input.mp4 -b:v 1500k output_1.5.mp4
- ffmpeg -i input.mp4 -b:v 2000k output_2.mp4
- ffmpeg -i input.mp4 -b:v 4000k output_4.mp4
4. Generate DASH files
- ffmpeg -i input_1.5.mp4 -i input_2.mp4 -i input_4.mp4 -map 0:v -map 1:v -map 2:v -c copy -f dash manifest.mpd
5. Move DASH files to Apache directory
- sudo cp -r dash_output/* /var/www/html/
6. Start Apache
- sudo systemctl start apache2
7. Open the stream

Author

Kai Mighty
Student ID: 4217377

## Results Summary

| Scenario | Condition | QoE Observation | MOS |
|--------|----------|----------------|-----|
| TBF | 2.5 Mbps | Moderate buffering, reduced quality | 3 |
| HTB | 2.5–5 Mbps | Smooth playback, stable quality | 4 |
| Policing | Packet loss (3.5 Mbps) | Stuttering, unstable playback | 2 |
