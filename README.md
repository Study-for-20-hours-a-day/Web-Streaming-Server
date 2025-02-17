# **📌 Web Video Server - A C++ and ROS 2 Based Web Video Streaming Server**  
🚀 **Supports H.264 / VP8 / VP9 / MJPEG / PNG, Ideal for Robots, Drones, and Remote Monitoring Applications**  

---

## **📌 Project Overview**  
**Web Video Server** is a high-performance **C++ and ROS 2-based video streaming server** that enables real-time **video transmission over HTTP**. It supports **multiple video encoding formats (H.264, VP8, VP9, MJPEG, PNG)** and integrates **FFmpeg (Libav) for optimized video compression**. Designed for **robotics, drones, and embedded systems**, it provides **low-latency video streaming and real-time snapshot capabilities**, making it ideal for remote monitoring applications.

### **🔹 Key Features**
✅ **Multi-Format Video Streaming**: Supports MJPEG, H.264, VP8, VP9, and PNG  
✅ **Optimized for Low-Latency Streaming**: Uses **FFmpeg (Libav)** for efficient encoding  
✅ **Seamless Web Compatibility**: Streams can be accessed using **HTML5 `<video>` tags**  
✅ **Multi-Client Support**: Handles multiple concurrent HTTP connections  
✅ **Dynamic ROS 2 Image Topic Subscription**: Automatically detects available camera topics  
✅ **QoS Optimization**: Adjustable settings to suit different network conditions  
✅ **Asynchronous HTTP Server**: Powered by **Boost.Asio** for high-concurrency handling  
✅ **Lightweight & Portable**: Runs on **embedded systems, edge devices, and cloud servers**  

---

## **📌 Supported Video Formats**
| Format  | Encoding Library | Use Case |
|---------|-----------------|----------|
| **MJPEG** | OpenCV | High compatibility, suitable for browser-based streaming |
| **H.264** | FFmpeg (libx264) | High compression, good for low-bandwidth streaming |
| **VP8** | FFmpeg (libvpx) | Low-latency, optimized for HTML5 `<video>` |
| **VP9** | FFmpeg (libvpx-vp9) | Higher compression, better quality than H.264 |
| **PNG** | OpenCV | Lossless compression, ideal for snapshots |

---

## **📌 Installation & Setup**
### **🔹 Prerequisites**
Ensure you have the following dependencies installed:
- **C++17 or later**
- **ROS 2 (Humble, Foxy, Galactic, or Rolling)**
- **FFmpeg (Libav)**
- **Boost.Asio**
- **OpenCV**
- **CMake 3.10+**

### **🔹 Clone & Build**
```bash
# Clone the repository
git clone https://github.com/yourusername/web_video_server.git
cd web_video_server

# Build using colcon
colcon build --symlink-install
```

### **🔹 Run the Web Video Server**
```bash
source install/setup.bash
ros2 run web_video_server web_video_server_node
```

---

## **📌 Usage**
### **🔹 Streaming Video**
Once the server is running, you can access the video stream using a web browser:  
```html
<video src="http://localhost:8080/stream?topic=/camera/image&type=h264" autoplay></video>
```
Or use `curl` to fetch a snapshot:
```bash
curl http://localhost:8080/snapshot?topic=/camera/image -o snapshot.jpg
```

### **🔹 Available Endpoints**
| Endpoint | Description |
|----------|-------------|
| `/` | List all available ROS image topics |
| `/stream?topic=<ros_topic>&type=<format>` | Stream video in the specified format |
| `/snapshot?topic=<ros_topic>` | Capture a snapshot of the current video frame |
| `/stream_viewer?topic=<ros_topic>` | Open an HTML5-based viewer for the stream |

Example:
```bash
# View available topics
curl http://localhost:8080/

# Stream an H.264 encoded video from /camera/image
curl http://localhost:8080/stream?topic=/camera/image&type=h264
```

---

## **📌 Configuration**
Modify `web_video_server` parameters in ROS 2:
```bash
ros2 param set /web_video_server port 9090  # Change HTTP port
ros2 param set /web_video_server default_stream_type mjpeg  # Set default encoding
ros2 param set /web_video_server server_threads 4  # Increase concurrency
```

---

## **📌 System Architecture**
- **`web_video_server.cpp`**: Core HTTP server logic, handles requests and manages video streams  
- **`h264_streamer.cpp`**: H.264 encoding using FFmpeg (libx264)  
- **`vp8_streamer.cpp`**: VP8 streaming, optimized for low-latency WebM playback  
- **`vp9_streamer.cpp`**: VP9 encoding for high compression and better quality  
- **`jpeg_streamers.cpp`**: MJPEG encoding for high-compatibility streaming  
- **`png_streamers.cpp`**: PNG image snapshots for high-fidelity captures  
- **`ros_compressed_streamer.cpp`**: Directly streams ROS-compressed image messages  

---

## **📌 Performance Optimizations**
✅ **Low-Latency Video Processing**: Uses **Boost.Asio for async HTTP handling**  
✅ **Real-Time Encoding**: `libx264`, `libvpx`, and OpenCV for fast frame processing  
✅ **QoS Optimization**: Supports **sensor_data QoS profile** for real-time applications  
✅ **Multi-Threaded Execution**: Uses ROS 2 **MultiThreadedExecutor** for concurrent handling  

---

## **📌 Applications**
🎯 **Robotics & Autonomous Systems**: Real-time monitoring for robots and drones  
🎯 **Remote Surveillance**: Low-latency video streaming for security applications  
🎯 **Embedded Systems**: Runs on **Jetson Nano, Raspberry Pi, Intel NUC**  
🎯 **Industrial IoT**: Edge computing solutions for **remote video analytics**  
🎯 **Automated Warehouses**: Video streaming for **robotic fleet monitoring**  

---

## **📌 Contributing**
We welcome contributions! Feel free to:
- Report issues and request features via **GitHub Issues**
- Fork the repo and submit **pull requests**
- Enhance video encoding optimizations and add new features

---

## **📌 License**
This project is released under the **BSD-3 License**.  
See the [LICENSE](LICENSE) file for more details.

---
