<p align="center">
    <img src="gallery/logo.png" width="150" height="150"/>
</p>

# Feniks - A computer based NVR with AI capabilities 

## Installation
* The installation process can be done effortlessly since all services are Dockerized and can be run by Docker-Compose in one single command. I' ve created a <a href="yaml-generator.html" target='_blank'>wizard</a> to make generating Docker-Compose file easy. 
    * Install Docker on your system: https://docs.docker.com/get-docker/
    * Install Docker Compose: https://docs.docker.com/compose/install/
    * Create docker-compose.yml file by using the <a href="yaml-generator.html" target='_blank'>wizard</a>
    * Open a terminal from the location where the generated docker-compose.yml file is located.
    * run 'docker-compose.yml' command to start Feniks.

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
* Feniks consists of 11 different services. Those are:
    * The FFmpeg Service For Live 7/24 Streaming, Snapshot and Recording (Python).
    * The Object Detection Service (Python).
    * The Snapshot Service (Python Multi-Process)
    * The Facial Recognition Service (Python, PyTorch).
    * The Plate Recognition Service (Golang).
    * The DeepStack Service (Python).
    * The Onvif Service (Golang).
    * The Cloud and Notification Service (GoLang).
    * The Web/Websockets Server Service (Golang).
    * The Web Application (Javascript/Typescript, Vue3, Quasar).
    * The Persistent RTSP Reader Service For AI (Python).

* Runs natively on Linux.
* Uses <a href="https://ffmpeg.org/" target="_blank">FFmpeg</a> to handle video, audio, snapshot, probing and streaming.
* Uses Redis as a main NoSql database and massage broker.

* MongoDB or SQLite is used for AI Events and query databases.

* The web application supports more than one user and node server.

* The UI app was developed by using Vue3 & <a href="https://quasar.dev/" target="_blank">Quasar</a>. It uses <a href="https://gridstackjs.com/" target="_blank">gridstack.js</a> to support highly customizable (like resize, dragging) video players.

* Supported Deep-Learning Frameworks: PyTorch, Tensorflow and the Nvidia Jetson Library and  can be selected from the Config page.
    * **PyTorch**: YOLOV5, [AlexNet](https://arxiv.org/abs/1404.5997), [VGG](https://arxiv.org/abs/1409.1556), [GoogLeNet](https://arxiv.org/abs/1409.4842), [MobileNetV3](https://arxiv.org/abs/1905.02244). For more information: [https://pytorch.org/vision/stable/models.html](https://pytorch.org/vision/stable/models.html)
    * **Tensorflow**: Resnet V2, SSD, Faster RCNN, EfficientDet. For more information: [https://tfhub.dev/tensorflow/collections/object_detection](https://tfhub.dev/tensorflow/collections/object_detection)
    * **Nvidia Jetson**: LPDNet, PeopleNet, ResNet-50, SSD. For more information: https://developer.nvidia.com/ai-models

* Automatic plate recognition performs very well since it has a built-in job scheduler and LPR docker containers can be scaled up horizontally.

* It has a built-in watchdog mechanism to monitor all processes and recover them.

* It can scan the whole network to find cameras which have RTSP broadcasts. You don’t need to find cameras’ IPs to register the system. All is done automatically.

* All running node services can be viewed on the UI app. All Services can be started/stopped by using the services page.

* The services are tested on x86 workstation, Dell Intel x86 laptop, Raspberry PI (ARM664) and Nvidia Jetson Nano.

* Broken / failed connections are shown in the information page. If a stream fails more than once in a given time, a notification will be sent to receivers (users) by the cloud provider service.

* Supported Stream Types are shown below:
    |   |  Hardware Demand | Latency  | Compatibility  |
    |---|---|---|---|
    | FLV         |  *     |  *     | ****   |
    | HLS         |  *     |  ***** | *****  |
    | WebSockets  |  ***** |  *     | *****  |
   
* Supported video codecs for both streaming and recording are:
    * H.264 (Software, VA-API, NVIDIA, INTEL, RASPBERRY PI)
    * H.265 (Software, VA-API, NVIDIA, INTEL, streaming is not supported since browsers and  RTMP servers don’t support HEVC hardware decoding)
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
   
* All AI events (Object Detection, Face Recognition, Plate Recognition) can be queried by date, time, camera, label and score. All those fields are all indexed and saved as denormalized entities to provide best read performance even for big data.

* It can store detected objects on clouds. Current cloud providers are: 
  * Google Gdrive 
  * Telegram

* Feniks supports 3 different motion detection methods, those are:
    * OpenCV: Superb accuracy precision but it costs relatively high CPU time
    * Imagehash:  good accuracy and high performance. It is suitable for low cost  devices like Raspberry PI or Jetson Nano 
    * PSNR: Similar to Imagehash

* Re-streaming via RTMP to reduce the number of connections to your camera
    <img src="gallery/loopback_arc.png" />
    

**Currently Developing Features List (Ordered By Release Date)**

1. Creating the Mobile Application (which are being developed right now by Quasar Framework)
2. Creating Central Hub System (which are being developed right now by using .Net Core) to access all nodes from a center. This project provides:
    * To manage thousands of cameras from one single point.
    * Making data transfer to nodes easy (like camera brand specific RTSP route).
    * Connect any node from the center.
    * Creating a total statistical information and meaningful dashboard.
    * Listing all failed cameras and forcing the user to take an immediate action.
    * Adding new REST endpoints to fully control Nodes remotely.
3. Adding Windows support. 
4. Positive/negative list support for facial recognition.
5. Adding camera location info registration support by Google Maps.
6. Adding Amazon S3, Microsoft OneDrive and Dropbox support as cloud providers.
7. Making ONVIF support more compatible and superior like PTZ (Pan-Tilt-Zoom Support for Cameras) support.
8 . Adding Tensorflow/PyTorch Pose Estimation deep-learning models.
