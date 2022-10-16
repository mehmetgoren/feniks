<p align="center">
    <img src="https://github.com/mehmetgoren/feniks/blob/main/logo.png" width="150" height="150"/>
</p>

# Feniks - A computer based NVR with AI capabilities 

* The installation process can be done effortlessly since all nine services are Dockerized and can be run by Docker-Compose in one single command.

* It consists of 11 different services. Those are:
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
* Uses FFmpeg to handle video, audio, snapshot, probing and streaming.
* Uses Redis as a main NoSql database and massage broker.

* MongoDB or SQLite is used for AI Events and query databases.

* The web application supports more than one user and node server.

* The UI app was developed by using Vue 3. It uses gridstack js to support highly customizable (like resize, dragging) video players.

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
    |FLV          |  *     |  ****  | ****   |
    | HLS         |  *     |  *     | *****  |
    | WebSockets  |  ***** |  ***** | *****  |
   
* Supported video codecs for both streaming and recording are:
    * H.264 (Software, NVIDIA, INTEL, RASPBERRY PI)
    * H.265 (Software, NVIDIA, INTEL, streaming is not supported since browsers don’t support HEVC hardware decoding)
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
    <img src="https://github.com/mehmetgoren/feniks/blob/main/loopback_arc.png" />
    

**Currently Developing Features List (Ordered By Release Date)**

1. Creating the Mobile Application (which are being developed right now by Quasar Framework)
2. Creating Central Hub System (which are being developed right now by using .Net Core) to access all nodes from a center. This project provides:
    * To manage thousands of cameras from one single point.
    * Making data transfer to nodes easy (like camera brand specific RTSP route).
    * Connect any node from the center.
    * Creating a total statistical information and meaningful dashboard.
    * Listing all failed cameras and forcing the user to take an immediate action.
    * Adding new REST endpoints to fully control Nodes remotely. 
3. Positive/negative list support for facial recognition.
4. Adding camera location info registration support by Google Maps.
5. Adding Amazon S3, Microsoft OneDrive and Dropbox support as cloud providers.
6. Making ONVIF support more compatible and superior like PTZ (Pan-Tilt-Zoom Support for Cameras) support.
7. Adding Tensorflow/PyTorch Pose Estimation deep-learning models.
