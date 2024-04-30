<p align="center">
    <img src="gallery/logo.png" width="150" height="150"/>
</p>

# Feniks - A computer based NVR with AI capabilities 
* Connect any source FFmpeg supports and start streaming with low latency. 
* Stream and record your videos 24/7 in both H.264 and H.265 formats directly from your browser..
* Detect 80 different objects, recognizes human faces, car plates and characters (OCR). There will be much more thanks to [CodeProject.AI](https://github.com/codeproject/CodeProject.AI-Server)
* Query your AI data fast & easy by date, time, camera, label, score and color.
* If you want more, develop your own custom AI service and easily integrate with Feniks. 

##### [Documentation Link](https://feniks.gitbook.io/doc)

## Installation
* The installation process can be done effortlessly since all services are dockerized and can be run by Docker-Compose in one single command. I' ve created a <a href="https://mehmetgoren.github.io/" target='_blank'>wizard</a> to make generating Docker-Compose file easy. 
    * Install Docker on your system: https://docs.docker.com/get-docker/
    * Install Docker Compose: https://docs.docker.com/compose/install/
    * Create docker-compose.yml file by using the <a href="https://mehmetgoren.github.io/" target='_blank'>wizard</a>
    * Open a terminal from the location where the generated docker-compose.yml file is located.
    * Run 'docker-compose up' command to start Feniks.
    * Open your browser and navigate to 'http://localhost:8080' after all service is initialized.

## Screenshots
<p align="center">
    <img src="gallery/login.jpg" width="200"/>
    <img src="gallery/stream_gallery1.jpg" width="400"/>
    <img src="gallery/stream_gallery2.jpg" width="400"/>
    <img src="gallery/stream_gallery3.jpg" width="280"/>
    <img src="gallery/zones.jpg" width="280"/>
    <img src="gallery/ai_clips.jpg" width="280"/>
    <img src="gallery/ai_data2.jpg" width="280"/>
    <img src="gallery/ai_data3.jpg" width="280"/>
    <img src="gallery/ai_data1.jpg" width="280"/>
    <img src="gallery/ai_coco_list.jpg" width="280"/>
    <img src="gallery/ai_images.jpg" width="280"/>
    <img src="gallery/settings.jpg" width="280"/>
    <img src="gallery/records1.jpg" width="280"/>
    <img src="gallery/records2.jpg" width="280"/>
    <img src="gallery/config.jpg" width="280"/>
    <img src="gallery/cloud.jpg" width="280"/>
    <img src="gallery/failed_cams.jpg" width="280"/>
    <img src="gallery/general1.jpg" width="280"/>
    <img src="gallery/general2.jpg" width="280"/>
    <img src="gallery/gpu.jpg" width="280"/>
    <img src="gallery/onvif.jpg" width="280"/>
</p>

## Technical Notes
* Feniks consists of 6 different services. Those are:
    * The FFmpeg Service For Live 7/24 Streaming, Snapshot and Recording (Python).
    * The Snapshot Service (Python Multi-Process)
    * The [CodeProject.AI](https://github.com/codeproject/CodeProject.AI-Server) Service(Python).
    * The Cloud and Notification Service (GoLang).
    * The Web/Websockets Server Service (Golang).
    * The Web Application (Javascript/Typescript, Vue3, Quasar).

* Runs natively on Linux.
* Uses <a href="https://ffmpeg.org/" target="_blank">FFmpeg</a> to handle video, audio, snapshot, probing and streaming.
* Uses Redis as a main NoSql database and message broker.

* MongoDB or SQLite is used for AI Events and query databases.

* The web application supports more than one user and node server.

* The UI app was developed by using Vue3 & <a href="https://quasar.dev/" target="_blank">Quasar</a>. It uses <a href="https://gridstackjs.com/" target="_blank">gridstack.js</a> to support highly customizable (like resize, dragging) video players.

* It has a built-in watchdog mechanism to monitor all processes and recover them.

* All running node services can be viewed on the UI app. All Services can be started/stopped by using the services page.

* The services are tested on x86 workstation, Dell Intel x86 laptop, Raspberry PI (ARM664) and Nvidia Jetson Nano.

* It supports multiple storages. You can assign any storage to any camera. 

* Broken / failed connections are shown in the information page. If a stream fails more than once in a given time, a notification will be sent to receivers (users) by the cloud provider service.

* Supported Stream Types are shown below:
    |   |  Hardware Demand | Latency  | Compatibility  |
    |---|---|---|---|
    | FLV         |  *     |  *     | ****   |
    | HLS         |  *     |  ***** | *****  |
    | WebSockets  |  ***** |  *     | *****  |
    | WebRTC      |  * |  *     | ****  |
   
* Supported video codecs for both streaming and recording are:
    * H.264 (Software, VA-API, NVIDIA, INTEL, RASPBERRY PI)
    * H.265 (Software, VA-API, NVIDIA, INTEL, HEVC streaming is supported thanks to [go2rtc](https://github.com/AlexxIT/go2rtc))
    * AV1 (Software, VA-API, NVIDIA, INTEL)
    * VP8 (Software, VA-API, NVIDIA, INTEL)
    * VP9 (Software, VA-API, NVIDIA, INTEL)
      
* Supported audio codecs  for both streaming and recording are:
    * MP3
    * AAC
    * AC3
    * DTS
    * ALAC
    
* Supported Video Container Formats:
    * MP4
    * WebM

* Supported Media Servers:
    * [go2rtc](https://github.com/AlexxIT/go2rtc) (H265 & H264). If you are unable to play H.265 streams or video records on your browser, please check out this [link](https://github.com/StaZhu/enable-chromium-hevc-hardware-decoding).
    * [SRS](https://github.com/ossrs/srs) (H264)
    * [LiveGo](https://github.com/gwuhaolin/livego) (H264)
    * [Node Media Server](https://github.com/illuspas/Node-Media-Server) (H264)
   
* All AI events (Object Detection, Face Recognition, Plate Recognition) can be queried by date, time, camera, label and score. All those fields are all indexed and saved as denormalized entities to provide best read performance even for big data.

* It can store detected objects on clouds. Current cloud providers are: 
  * Google Gdrive 
  * Telegram

* Feniks supports 3 different motion detection methods, those are:
    * OpenCV: Superb accuracy precision but it costs relatively high CPU time
    * Imagehash:  good accuracy and high performance. It is suitable for low cost  devices like Raspberry PI or Jetson Nano 
    * PSNR: Similar to Imagehash

* Re-streaming via media server to reduce the number of connections to your camera
    <img src="gallery/loopback_arc.png" />