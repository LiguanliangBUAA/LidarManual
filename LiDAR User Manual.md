### 1. RoboSense E1

This tutorial refers to running the LiDAR in a local environment. It can also be run in environments such as Docker and PIXI. (https://github.com/alvgaona/lidarodom)

#### 1.1 Environment Introduction

Ubuntu 22.04, Ros2 Humble, WireShark (Optional, helps to confirm if the interface functions is operational, enables more convenient data recording)

#### 1.2 LiDAR System

RoboSense E1, Vehicle Ethernet Harness, Interface Box, Power Cable, Signal Cable, RJ45 to USB Cable

![image-20251201100955673](LiDAR User Manual.assets/image-20251201100955673.png)

#### 1.3 Software download

##### 1.3.1 RoboSense SDK

This link https://github.com/RoboSense-LiDAR/rslidar_sdk provides the installation tutorial.

1. Create a workspace and a "src" folder.

2. Confirm that the versions of YAML and libpcap meet the requirements.

3. Open a terminal in "src" folder. And run the following commands:

   ```
   git clone https://github.com/RoboSense-LiDAR/rslidar_sdk.git
   cd rslidar_sdk
   git submodule init
   git submodule update
   ```

4. Clone msg package too.

   ```
   git clone https://github.com/RoboSense-LiDAR/rslidar_msg.git
   ```

5. Return to the workspace folder, compile and run it to test if the SDK is installed successfully.

   ```
   colcon build
   source install/setup.bash
   ros2 launch rslidar_sdk start.py
   ```

##### 1.3.2 RSView

Download RSView via this link: https://www.robosense.ai/en/resources-160. After extracting the file, run the "./run_rsview.sh" command in the folder to launch it.

#### 1.4 Usage Steps

##### 1.4.1  Pre-System Preparation

1. Open the network settings in the system settings. Create a new wired connection settings -- RoboSense.
   ![image-20251201101505437](LiDAR User Manual.assets/image-20251201101505437.png)
2. Set the name as you want. In IPv4 field, set IPv4 Method "Manual". In Addresses field, set address "192.168.1.102", netmask "255.255.255.0", Gateway empty. Click "Apply".
   ![image-20251201102142524](LiDAR User Manual.assets/image-20251201102142524.png)

##### 1.4.2 Device Connection

1. As shown in the figure, connect all devices. At this point, the interface box displays one green light (indicating a normal signal cable connection) and one red light (steady on, indicating the power cable is connected).
   ![image-20251201102949451](LiDAR User Manual.assets/image-20251201102949451.png)
2. Click the button on the box to activate the LiDAR. After a few seconds, observe that both lights start blinking, indicating the LiDAR has begun operating.

##### 1.4.3 Signal Acquisition

1. Switch the wired connection to "RoboSense".
2. Open a terminal and enter the "ip a" command to check the LiDAR interface name.
   ![image-20251201104947710](LiDAR User Manual.assets/image-20251201104947710.png)
3. Optional: Open Wireshark, choose the interface. It can be seen that the data transmission is normal.
   ![image-20251201105618203](LiDAR User Manual.assets/image-20251201105618203.png)

##### 1.4.4 Point Cloud Visualization

1. RoboSense SDK: Open a terminal in workspace. Type the following commands:

   ```
   source install/setup.bash
   ros2 launch rslidar_sdk start.py
   ```

   Point clouds can be seen:

   ![image-20251201113230565](LiDAR User Manual.assets/image-20251201113230565.png)

2. RSView: Open a terminal in the folder where it is downloaded. Type the following commands:

   ```
   ./run_rsview.sh
   ```

   Click "Open Sensor". Choose the right "Sensor Type". Click "OK". And another "OK". 

   ![image-20251201113709324](LiDAR User Manual.assets/image-20251201113709324.png)

   ![image-20251201113907403](LiDAR User Manual.assets/image-20251201113907403.png)

   Point clouds can be seen:

   ![image-20251201114019687](LiDAR User Manual.assets/image-20251201114019687.png)

3. If you can't see point cloud, and wireshark shows good. It could be your firewall.

### 2. Livox MID360

#### 2.1 Environment Introduction

Ubuntu 22.04, Ros2 Humble, WireShark (Optional, helps to confirm if the interface functions is operational, enables more convenient data recording)

#### 2.2 LiDAR System

Livox MID360, ROSbot, PowerLines for both Livox MID360 and ROSbot, Livox Aviation Connector 1-to-3 Splitter Cable, RJ45 to USB Cable

![image-20251201130553678](LiDAR User Manual.assets/image-20251201130553678.png)

#### 2.3 Software download

##### 2.3.1 Livox Driver

Use Livox ROS Driver 2, which can be downloaded with link: https://github.com/Livox-SDK/livox_ros_driver2.

1. Download Livox-SDK2. The tutorial link is: https://github.com/Livox-SDK/Livox-SDK2. Run following commands in a terminal:

   ```
   # install cmake
   sudo apt install cmake
   # install Livox-SDK2
   git clone https://github.com/Livox-SDK/Livox-SDK2.git
   cd ./Livox-SDK2/
   mkdir build
   cd build
   cmake .. && make -j
   sudo make install
   ```

   **Note :**
    The generated shared library and static library are installed to the  directory of "/usr/local/lib". The header files are installed to the  directory of "/usr/local/include".

2. Create a workspace and a "src" folder.

3. Open a terminal in "src" folder. And run the following commands:

   ```
   git clone https://github.com/Livox-SDK/livox_ros_driver2.git ws_livox/src/livox_ros_driver2
   ```

4. Change the config file: open src/livox_ros_drive2/config/MID360_config.json. Change lidar ip.

   ```json
   # original
   # ...
   "lidar_configs" : [
       {
         "ip" : "192.168.1.12",
   # ...
   # Change into
   # ...
   "lidar_configs" : [
       {
         "ip" : "192.168.1.122",
   # ...
   ```

5. Return to the workspace folder, compile and run it to test if the SDK is installed successfully.

   ```
   colcon build
   source install/setup.bash
   ros2 launch livox_ros_driver2 rviz_MID360_launch.py 
   ```

##### 2.3.2 LivoxViewer2

Download LivoxViewer2 via this link: https://www.livoxtech.com/downloads. After extracting the file, run the "./LivoxViewer2.sh" command in the folder to launch it.

#### 2.4 Usage Steps

##### 2.4.1  Pre-System Preparation

1. Open the network settings in the system settings. Create a new wired connection settings -- Livox, as the photo shown in 1.4.1.
2. Set the name as you want. In IPv4 field, set IPv4 Method "Manual". In Addresses field, set address "192.168.1.5", netmask "255.255.255.0", Gateway empty. Click "Apply".
   ![image-20251201155434740](LiDAR User Manual.assets/image-20251201155434740.png)

##### 2.4.2 Device Connection

1. As shown in the figure, connect all devices. Connect the power cable to the ROSbot as shown in the figure to use ROSbot power supply for powering the LiDAR.
   ![image-20251201161016216](LiDAR User Manual.assets/image-20251201161016216.png)
2. Turn the ROSbot on. The LiDAR starts to vibrate proving it works.

##### 2.4.3 Signal Acquisition

1. Switch the wired connection to "Livox".
2. Open a terminal and enter the "ip a" command to check the LiDAR interface name.
   ![image-20251201162000158](LiDAR User Manual.assets/image-20251201162000158.png)
3. Optional: Open Wireshark, choose the interface. It can be seen that the data transmission is normal.
   ![image-20251201162032650](LiDAR User Manual.assets/image-20251201162032650.png)

##### 2.4.4 Point Cloud Visualization

1. RoboSense SDK: Open a terminal in workspace. Type the following commands:

   ```
   source install/setup.bash
   ros2 launch livox_ros_driver2 rviz_MID360_launch.py 
   ```

   Point clouds can be seen:

   ![image-20251201162143899](LiDAR User Manual.assets/image-20251201162143899.png)

2. RSView: Open a terminal in the folder where it is downloaded. Type the following commands:

   ```
   ./LivoxViewer2.sh
   ```

   Choose the Adapter to 192.168.1.5. Then the LiDAR and PointCloud will be seen.

   ![image-20251201162345034](LiDAR User Manual.assets/image-20251201162345034.png)

### 3. Unitree 4D LiDAR L2

#### 3.1 Environment Introduction

Ubuntu 22.04, Ros2 Humble, WireShark (Optional, helps to confirm if the interface functions is operational, enables more convenient data recording)

#### 3.2 LiDAR System

Unitree 4D LiDAR L2, LiDAR Power Line, RJ45 signal cable, LiDAR charger, RJ45 to USB Cable, Chinese-to-European socket adapter, the mat coming with LiDAR (always remember the LiDAR should operate on the mat, as it will vibrate during operation and the mat is required for buffering)

![image-20251201171410242](LiDAR User Manual.assets/image-20251201171410242.png)

#### 3.3 Software download

##### 3.3.1 Unilidar SDK2

Use Unilidar SDK2. The tutorial link is: https://github.com/unitreerobotics/unilidar_sdk2?tab=readme-ov-file. The download link is: https://github.com/unitreerobotics/unilidar_sdk2.git.

1. Install PCL with the following commands:

   ```
   sudo apt update
   sudo apt install libpcl-dev
   ```

2. 
   Create a workspace folder and a "src" folder. Download Unilidar SDK2 in the "src" folder: 

   ```
   # Create workspace
   mkdir ws/src
   cd ws/src
   # Download SDK
   git clone https://github.com/unitreerobotics/unilidar_sdk2.git
   # remove unitree_lidar_ros
   cd unilidar_sdk2
   rm -rf unitree_lidar_ros
   ```

   **Note :**
    In the package, "unitree_lidar_ros" need to be deleted, or it will cause compilation errors.

3. Return to the workspace folder, compile and run it to test if the SDK is installed successfully.

   ```
   colcon build
   source install/setup.bash
   ros2 launch unitree_lidar_ros2 launch.py
   ```

##### 3.3.2 LivoxViewer2

You can download Unilidar Point Cloud Software with the link: https://www.unitree.com/download/L2. Because it's an exe file, it will not be used here.

#### 3.4 Usage Steps

##### 3.4.1  Pre-System Preparation

1. Open the network settings in the system settings. Create a new wired connection settings -- Unitree, as the photo shown in 1.4.1.
2. Set the name as you want. In IPv4 field, set IPv4 Method "Manual". In Addresses field, set address "192.168.1.2", netmask "255.255.255.0", Gateway "192.168.1.1". Click "Apply".
   ![image-20251201174958006](LiDAR User Manual.assets/image-20251201174958006.png)

##### 3.4.2 Device Connection

1. As shown in the figure, connect all devices. The LiDAR will begin to rotate.
   ![image-20251201175137757](LiDAR User Manual.assets/image-20251201175137757.png)

##### 3.4.3 Signal Acquisition

1. Switch the wired connection to "Unitree".
2. Open a terminal and enter the "ip a" command to check the LiDAR interface name.
   ![image-20251201175416084](LiDAR User Manual.assets/image-20251201175416084.png)
3. Optional: Open Wireshark, choose the interface. It can be seen that the data transmission is normal.
   ![image-20251201175438785](LiDAR User Manual.assets/image-20251201175438785.png)

##### 3.4.4 Point Cloud Visualization

1. Unilidar SDK2: Open a terminal in workspace. Type the following commands:

   ```
   source install/setup.bash
   ros2 launch unitree_lidar_ros2 launch.py
   ```

   Point clouds can be seen:

   ![image-20251201175555750](LiDAR User Manual.assets/image-20251201175555750.png)

