

# 📖 Installation Guide

This document describes the configuration of environment variables used in the `nginx.config.template`.
Each variable controls an aspect of the **RTMP server**, **HLS streaming**, **Nginx core configuration**, or **HTTP headers**.

The goal of this guide is to provide a clear understanding of what each parameter does, its default value, and how it affects the streaming server.

---

## 🔧 RTMP Server Configuration

The **RTMP server** is responsible for receiving live streams (commonly from broadcasting software like OBS) and handling the initial ingestion of video data. These variables define how the RTMP service binds to the host machine and the ports it uses.

| Variable    | Default Value | Description                                                                                                  |
| ----------- | ------------- | ------------------------------------------------------------------------------------------------------------ |
| `HOST`      | `0.0.0.0`     | The IP address on which the RTMP/HTTP servers will listen. `0.0.0.0` means all available network interfaces. |
| `RTMP_PORT` | `1935`        | The port used for the **RTMP server** (default RTMP port).                                                   |
| `HLS_PORT`  | `8080`        | The port where **HLS (HTTP Live Streaming)** content will be served.                                         |

---

## 🌐 Backend and Frontend URLs

These variables define where the backend services and frontend interface of the system are located. They are useful for validating streams, sending events, or connecting the user interface to the streaming service.

| Variable       | Default Value         | Description                                                                 |
| -------------- | --------------------- | --------------------------------------------------------------------------- |
| `URL_BACKEND`  | `http://0.0.0.0:3000` | Backend URL, where validations or stream-related events can be sent.        |
| `URL_FRONTEND` | `http://0.0.0.0:3230` | Frontend URL, used to connect the web interface with the streaming service. |

---

## ⚙️ Nginx Core Configuration

These variables control the **performance and scalability** of the Nginx server. They define how many worker processes will be spawned and how many simultaneous connections each worker can handle.

| Variable                   | Default Value | Description                                                                                           |
| -------------------------- | ------------- | ----------------------------------------------------------------------------------------------------- |
| `NGINX_WORKER_PROCESSES`   | `auto`        | Number of worker processes. `auto` lets Nginx automatically detect the number of available CPU cores. |
| `NGINX_WORKER_CONNECTIONS` | `1024`        | Maximum number of simultaneous connections each worker process can manage.                            |

---

## 📡 RTMP Performance

The RTMP performance configuration affects how video data is chunked and transmitted over the network. Larger chunk sizes can reduce network overhead, but may slightly increase latency.

| Variable          | Default Value | Description                                                                                        |
| ----------------- | ------------- | -------------------------------------------------------------------------------------------------- |
| `RTMP_CHUNK_SIZE` | `4096`        | Size of RTMP data chunks (in bits). A higher value reduces packet overhead but may affect latency. |

---

## 🎬 HLS Configuration (HTTP Live Streaming)

HLS is used to serve video over HTTP by breaking streams into small `.ts` files and playlists (`.m3u8`). These variables define how video is segmented, playlist duration, and available streaming qualities (bitrates).

| Variable              | Default Value | Description                                                                               |
| --------------------- | ------------- | ----------------------------------------------------------------------------------------- |
| `HLS_FRAGMENT`        | `1`           | Duration (in seconds) of each `.ts` video fragment.                                       |
| `HLS_PLAYLIST_LENGTH` | `60`          | Total length (in seconds) of the playlist `.m3u8`.                                        |
| `HLS_FRAGMENT_NAMING` | `sequential`  | Naming method for HLS fragments. `sequential` means files are named in consecutive order. |
| `HLS_LOW_BANDWIDTH`   | `500000`      | Low-bitrate HLS variant (in bits per second).                                             |
| `HLS_MID_BANDWIDTH`   | `1000000`     | Medium-bitrate HLS variant (in bits per second).                                          |
| `HLS_HI_BANDWIDTH`    | `3000000`     | High-bitrate HLS variant (in bits per second).                                            |

---

## 📑 HTTP Headers

The HTTP server defines security and caching policies for the content served. These headers are especially important for allowing cross-origin access and controlling caching behavior of HLS files.

| Variable        | Default Value                         | Description                                                                                                |
| --------------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `CORS_ORIGIN`   | `*`                                   | Defines which origins are allowed to access the content. `*` allows all origins (public access).           |
| `CACHE_CONTROL` | `no-cache, no-store, must-revalidate` | Cache policy for HLS content. This disables caching to ensure the most recent fragments are always served. |

---------------------------------------

# ⚙️ RTMP Configuration (Input Protocol)

### **`worker_processes auto`**

* **What it does:** Nginx automatically creates the optimal number of worker processes based on the number of available CPU cores.
* **Effect on streaming:** Improves performance and allows handling multiple simultaneous streams.

### **`worker_connections 1024`**

* **What it does:** Each worker process can handle up to 1024 simultaneous connections.
* **Effect on streaming:** Enables many viewers to watch your stream at the same time.

### **`chunk_size 4096`**

* **What it does:** Defines the RTMP data chunk size (4KB).
* **Effect on streaming:**

  * **Low value (1–2KB):** Lower latency but higher network overhead.
  * **High value (8–16KB):** Higher latency but better network efficiency.
  * **Current (4KB):** Balanced trade-off between latency and performance.

---

# 🎬 HLS Configuration (Output Protocol)

### **`hls_fragment 1s`**

* **What it does:** Each `.ts` segment (video fragment) lasts exactly 1 second.
* **Effect on streaming:**

  * **0.5s:** Very low latency (2–3 seconds) but generates more files = higher overhead.
  * **1s (current):** Low latency (3–5 seconds), balanced option.
  * **2s:** Medium latency (5–8 seconds) with improved stability.
  * **4s:** High latency (10–15 seconds) but very stable.

### **`hls_playlist_length 3s`**

* **What it does:** The `.m3u8` playlist contains only 3 segments.
* **Effect on streaming:**

  * **1s:** Minimum latency, but risk of interruptions with network issues.
  * **2s:** Very low latency, slightly more stable.
  * **3s (current):** Low latency with good stability.
  * **5s:** Medium latency, highly stable.
  * **10s:** High latency, maximum stability.

### **`hls_fragment_naming sequential`**

* **What it does:** Segments are named sequentially (1.ts, 2.ts, 3.ts...).
* **Alternatives:**

  * **`system`:** Uses system timestamp.
  * **`timestamp`:** Uses stream timestamp.
* **Effect:** Affects only file naming, not latency.

### **`hls_cleanup on`**

* **What it does:** Automatically deletes old `.ts` files.
* **Effect:** Keeps disk usage low, does not affect latency.

### **`hls_type live`**

* **What it does:** Configures HLS for **live streaming**.
* **Alternatives:**

  * **`event`:** For one-time events (segments are not deleted).
  * **`vod`:** For video on demand.
* **Effect:** `live` is optimal for continuous streaming.

---

# 🌐 HTTP Configuration (Web Server)

### **CORS and Cache Headers**

* **`Access-Control-Allow-Origin *`** → Allows any website to play your stream.
* **`Cache-Control no-cache`** → Prevents browsers from caching stream data, ensuring fresh segments are always fetched.

---

# 📊 How to Adjust for Different Needs

### 🎯 **For Minimum Latency (Gaming, Sports):**

```nginx
hls_fragment 0.5s;
hls_playlist_length 1.5s;
```

**Result:** Latency around 2–3 seconds, less stable.

### 🎯 **For Maximum Stability (Important Events):**

```nginx
hls_fragment 2s;
hls_playlist_length 6s;
```

**Result:** Latency around 6–8 seconds, very stable.

### 🎯 **For Balanced Performance (Current Setup):**

```nginx
hls_fragment 1s;
hls_playlist_length 3s;
```

**Result:** Latency around 3–5 seconds, good stability.

---

# ⚠️ Key Considerations

### **Bandwidth**

* Smaller fragments = More files = More HTTP requests.
* Larger fragments = Fewer files = Fewer HTTP requests.

### **Stability vs Latency**

* **Low latency:** Better user experience.
* **High stability:** Fewer interruptions during streaming.

### **Server Resources**

* Smaller fragments = Higher disk I/O.
* Larger fragments = Lower disk I/O.

