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

## DASH Packaging

Labb38 Manifest

-ffmpeg -i Lab38_1_5.mov -i Lab38_2.mov -i Lab38_4.mov \
-map 0:v -map 1:v -map 2:v -c copy -f dash \
-init_seg_name 'init_$RepresentationID$.m4s' \
-media_seg_name 'chunk_$RepresentationID$_$Number$.m4s' \
Lab38_manifest.mpd

Landscape Manifest
- ffmpeg -i landscape_1mbps.mp4 -i landscape_2mbps.mp4 -i landscape_4mbps.mp4 \
-map 0:v -map 1:v -map 2:v -c copy -f dash \
-init_seg_name 'init_$RepresentationID$.m4s' \
-media_seg_name 'chunk_$RepresentationID$_$Number$.m4s' \
landscape_manifest.mpd

## Web Server Setup
- sudo apt install apache2
sudo cp -r dash_output/* /var/www/html/
sudo systemctl start apache2

## IPERF Testing
- iperf -s -p 5001

Run Client (Ubuntu)
- iperf -c SERVER_IP -p 5001 -b 1M -t 600

## Traffic Control Scenarios

Scenario A - TBF
- sudo tc qdisc add dev eth0 root tbf rate 2.5mbit burst 20kb latency 50ms

Scenario B - HTB
- sudo tc qdisc add dev eth0 root handle 1: htb default 11

sudo tc class add dev eth0 parent 1: classid 1:1 htb rate 2.5mbit

sudo tc class add dev eth0 parent 1:1 classid 1:10 htb rate 1mbit ceil 2.5mbit prio 1

sudo tc class add dev eth0 parent 1:1 classid 1:11 htb rate 1.5mbit ceil 2.5mbit prio 2

sudo tc filter add dev eth0 protocol ip parent 1: prio 1 u32 \
match ip dport 5001 0xffff flowid 1:10

Scenario C – Traffic Policing (Client Side)
- sudo tc qdisc add dev enp0s3 handle ffff: ingress

sudo tc filter add dev enp0s3 parent ffff: protocol ip prio 1 u32 \
match u32 0 0 police rate 3.5mbit burst 20k drop flowid :1

## Results Summary

| Scenario | Condition | QoE Observation | MOS |
|--------|----------|----------------|-----|
| TBF | 2.5 Mbps | Moderate buffering, reduced quality | 3 |
| HTB | 2.5–5 Mbps | Smooth playback, stable quality | 4 |
| Policing | Packet loss (3.5 Mbps) | Stuttering, unstable playback | 2 |

Author
Kai Mighty 
Student ID: 4217377 
