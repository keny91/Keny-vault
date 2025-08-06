#bandwidth #requirements #videostreams

## 📺 Typical Video Streaming Bandwidth Usage

### 🔢 Bandwidth by Quality Level (Video Only)

|Resolution|Framerate|Bitrate (avg)|Bandwidth per hour|
|---|---|---|---|
|240p (SD low)|30 fps|300–500 kbps|~150–250 MB|
|360p (SD)|30 fps|500–1 Mbps|~250–450 MB|
|480p (SD high)|30 fps|1–2 Mbps|~450–900 MB|
|720p (HD)|30–60 fps|2–4 Mbps|~900 MB–1.8 GB|
|1080p (Full HD)|60 fps|4–8 Mbps|~1.8–3.6 GB|
|1440p (QHD)|60 fps|8–16 Mbps|~3.6–7.2 GB|
|2160p (4K)|60 fps|15–25 Mbps|~6.8–11.25 GB|
|4320p (8K)|60 fps|50–100 Mbps|~22–45 GB|

🎯 These values vary based on:

- **Codec** used (H.264 vs H.265/HEVC vs AV1)
    
- **Content complexity** (static scenes use less than action-packed)
    
- **Streaming service compression settings** (YouTube vs Netflix vs Twitch)

---

## 🎧 Audio-Only Streams

|Format|Bitrate|Bandwidth per hour|
|---|---|---|
|Low quality MP3|64 kbps|~28 MB|
|Typical MP3/AAC|128–192 kbps|~56–84 MB|
|High-quality AAC|256 kbps|~112 MB|
|Lossless (FLAC)|500–1,000 kbps|~225–450 MB|
|Hi-Res Audio|1.5–3 Mbps|~675 MB–1.35 GB|

---

## 🎥 Common Streaming Services (Estimates)

|Service|Resolution|Bitrate Range|Notes|
|---|---|---|---|
|**YouTube**|1080p60|~3–6 Mbps|Uses VP9 or AV1|
|**Netflix**|1080p|~3–7 Mbps|Adaptive bitrate streaming (ABR)|
|**Netflix**|4K HDR|~15–25 Mbps|Uses H.265/HEVC, Dolby Vision|
|**Twitch**|720p60|~3.5–5 Mbps (ingest)|Partners may go higher|
|**Disney+**|4K HDR|~15–20 Mbps|HEVC/HDR10+|
|**Zoom/Meet**|720p|~1–2 Mbps (2-way)|Audio + video, depends on usage|

## 🧮 Quick Calculation: Data Usage Per Hour

To estimate:

```
Data (MB/hr) ≈ Bitrate (Mbps) × 450
```

(Why 450? Because:  
1 Mbps = 0.125 MB/s  
→ 0.125 MB/s × 3600 s = 450 MB/hr)

Example:

- 6 Mbps stream → 6 × 450 = ~2.7 GB/hr
    

---
#todo
## 🛠️ 1. Check Your Available Bandwidth (Speed Test)

### 🔹 CLI Speed Test with `speedtest-cli`

Install:

```
# Debian/Ubuntu
sudo apt install speedtest-cli

# Or with pip
pip install speedtest-cli
```

Run:
```
speedtest
```

You’ll get:
```
Download: 94.67 Mbit/s
Upload: 31.85 Mbit/s
```


## 🛠️ 2. Monitor Real-Time Bandwidth Usage (All Traffic)

### 🔹 `nload` (Real-time Network Throughput Monitor)

Install:

```
sudo apt install nload
```

Run: 
```
nload
```

It shows incoming/outgoing bandwidth per network interface (`eth0`, `wlan0`, etc.).

---

## 🛠️ 3. Monitor a Specific Process (e.g., Video Stream)

### 🔹 `iftop` (Bandwidth per connection/IP)

Install:

```
sudo apt install iftop
```

Run:
```
sudo iftop -i wlan0      # or eth0 depending on your interface
```

You’ll see a live table of active connections and their traffic usage.

## 🛠️ 4. Advanced: Measure Streaming Bandwidth with `ffmpeg`

If you're testing a stream (e.g., webcam, RTSP, or YouTube), use:
```
ffmpeg -i <input_url> -f null -
```

This will show actual stream bitrate while discarding output:
```
sudo apt install bmon
bmon
```


## 📊 How to Compare?

1. Run `speedtest` to find your max available bandwidth.
    
2. Run `nload` or `iftop` while streaming a video.
    
3. Note the average bandwidth used.
    
4. Use ratio to estimate load:
   
```
% Usage = (Streaming Bitrate / Speedtest Download) × 100
```

Example:

- Stream uses 4 Mbps.
    
- You have 20 Mbps down.
    
- → 4 / 20 = 20% of your available bandwidth used.

