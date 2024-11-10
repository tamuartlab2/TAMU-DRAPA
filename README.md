<h1>DRAPA:  Dataset for Robotic Automation and Precision Agriculture in Cotton and Peanut Fields</h1>

<p align="center">
<a href="https://www.tamu.edu/"><img src="Images/tamu_logo.png" alt="Texas A&M University" height="200px" width="1000px">
  
Yuan Wei<sup>1</sup>, Neha Vemula<sup>1</sup>, Joe Johnson<sup>2</sup>, Jose Landivar<sup>3</sup>, Oscar Fernandez<sup>3</sup>, Shrikrishna
Gad<sup>1</sup>, Dugan Um<sup>4</sup>, Robert Hardin<sup>5</sup>, John Cason<sup>6</sup>, Mahendra Bhandari<sup>3</sup>, Muthukumar
Bagavathiannan<sup>2</sup>, and Kiju Lee<sup>7,1</sup>

<a href="https://engineering.tamu.edu/mechanical/index.html">J. Mike Walker ’66 Department of Mechanical Engineering<sup>1</sup>;
<a href="https://ccag.tamu.edu/">Texas A&M AgriLife Center at Corpus Christi<sup>2</sup>;
<a href="https://soilcrop.tamu.edu/">Department of Soil and Crop Sciences<sup>3</sup>;
<a href="https://www.tamucc.edu/engineering/">College of Engineering and Computer Science<sup>4</sup>;
<a href="https://baen.tamu.edu/">Department of Biological & Agricultural Engineering<sup>5</sup>;
<a href="https://stephenville.tamu.edu/">Texas A&M AgriLife Center at Stephenville<sup>6</sup>;
<a href="https://engineering.tamu.edu/etid/index.html">Department of Engineering Technology & Industrial Distribution<sup>7</sup>

## Overview
Dataset for Robotic Automation and Precision Agriculture (DRAPA) is a new dataset including multimodal sensor data collected from a custom-developed mobile robot. The dataset includes GPS data, RGB-D images, data from the inertial measurement unit (IMU), and 2D LiDAR data.

## Platform and Sensor suit for data collection
We employed mobile robotic platforms for data collection. Each robot was built on a commercial chassis (AION R1) with fully customized electronics and sensors. The main processor was Raspberry Pi 4 Model B with 8 GB RAM and quad-core Cortex-A72 (ARM v8) 1.5 GHz 64-bit CPU. It operates within a Ubuntu 22.04 operating system, utilizing Robot Operating System 2 (ROS2) for robotic control and software integration.

* RGBD Camera: Provides Red-Green-Blue color data and depth information.
* GNSS/GPS Sensor: Offers Global Navigation Satellite System data for precise positioning.
* 2D LiDAR Sensor: Measures distances in a 2D plane using laser detection.
* Inertial Measurement Unit (IMU): Comprising:
  * Compass: Provides heading or orientation.
  * Gyroscope: Measures angular velocity.
  * Accelerometer: Measures linear acceleration.
This suite allows for visual, spatial, and positional data collection for various applications.

<p align="center">
  
![Platform and Sensor suit for data collection](/Images/robot_sensors.png)

## Recorded data folder structure
<pre>
Data
├── crop_field_data_College_Station
│   ├── CS_cotton_2023
│   │   ├── Depth_data                               // Contains depth images in .png
│   │   ├── RGB_data                                 // Contains RGB images in .jpg
│   │   └── rosbag2_2023_06_10-12_17_11              // Contains metadata and rosbag file
│   │       ├── metadata.yaml                        // Records sensor configurations and data acquisition parameters
│   │       └── rosbag2_2023_06_10-12_17_11_0.db3    // Raw data with timestamped messages for multi-sensor analysis
│   ├── CS_cotton_2024
│   ├── CS_peanut_2023
│   └── CS_peanut_2024
└── crop_field_data_Corpus_Christi
    ├── 2023
    └── 2024
</pre>



## Overview of the Data: ROS Topics, Message Types, and Descriptions

| No. | Topic                                      | Message Type                   | Description                                                                                     |
|-----|--------------------------------------------|--------------------------------|-------------------------------------------------------------------------------------------------|
| 1   | `/Localization/GPS`                        | `sensor_msgs/msg/NavSatFix`    | Provides GPS data (latitude, longitude, altitude) for robot positioning.                        |
| 2   | `/Localization/Odom`                       | `nav_msgs/msg/Odometry`        | Delivers odometry data (position, velocity) for navigation.                                     |
| 3   | `/Roboclaw/Odom`                           | `nav_msgs/msg/Odometry`        | Supplies odometry data from the Roboclaw motor controller for movement tracking.                |
| 4   | `/Teensy/GPS`                              | `sensor_msgs/msg/NavSatFix`    | Offers GPS data from the Teensy microcontroller for enhanced localization.                      |
| 5   | `/Teensy/IMU`                              | `sensor_msgs/msg/Imu`          | Contains orientation, angular velocity, and acceleration data from an IMU.                      |
| 6   | `/camera/aligned_depth_to_color/image_raw` | `sensor_msgs/msg/Image`        | Provides raw image data for visual information and obstacle detection.                          |
| 7   | `/ra_camera`                               | `sensor_msgs/msg/CompressedImage` | Contains compressed image data for efficient transmission.                                  |
| 8   | `/scan`                                    | `sensor_msgs/msg/LaserScan`    | Provides range data from laser scanners for mapping.                                            |



## Accessing and Analyzing Data from the ROS Bag

This section describes how to initiate data playback from ROS bag files. To start, open a terminal and run:

```bash
ros2 bag play <rosbag_file_name>
```
This command replays messages in their original sequence and timing, opening the database in read-only mode and publishing messages at the recorded rate. Users can adjust playback speed and control playback using the following options:

* Pause/Resume: Press SPACE to pause or resume playback.
* Next Message: Press CURSOR RIGHT to advance to the next message.
* Speed Adjustment: Use CURSOR UP or CURSOR DOWN to increase or decrease playback speed by 10%.

Example screenshot of the terminal running rosbag file:

For detailed data analysis, users can subscribe to specific topics by using the ros2 topic echo command followed by the topic name in another terminal, for example:
```bash
ros2 topic echo <topic_name>
```
Example screenshot of the terminal with topic names:


## Full data download link:
Drive link

