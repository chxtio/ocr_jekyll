---
title: "Sonar Viz Bot User Manual"
date: 2025-07-25
---

<!-- # Table of Contents

- [1. Software Setup](#1-software-setup)
    - [1.0 Join the Github Organizations](#10-join-the-github-organizations)
    - [1.1 Recommended Directory Structure](#11-recommended-directory-structure)
    - [1.2 Setting Up Git, GitHub, and SSH](#12-setting-up-git-github-and-ssh)
    - [1.3 Create Initial Directory Structure](#13-create-initial-directory-structure)
    - [1.4 OCR Docker](#14-ocr-docker)
    - [1.5 Differential Drive Robot](#15-differential-drive-robot)
    - [1.6 Raspberry Pi Setup](#16-raspberry-pi-setup)
- [2. Electrical Setup](#2-electrical-setup)
    - [2.1 Software](#21-software)
    - [2.2 L293D Motor Driver](#22-l293d-motor-driver) -->

# Project Introduction

This instruction manual outlines the process of designing and building the *Sonar Viz Bot*- a training project intended to introduce new OCR members to the engineering design process. It aims to quickly develop the core skills and competencies for rookies to meaningfully contribute to club projects and eventually compete in the University Rover Challenge (URC).

<!-- This instruction manual outlines the process of designing and building *Sonar Viz Bot*- a training project intended to help new OCR members quickly develop the core skills and competencies to meaningfully contribute to club projects... and eventually compete in the University Rover Challenge (URC)! -->


<!-- <img src="https://i.imgur.com/QXUko01.png" width="400" > -->

<div style="text-align: center;">
  <img src="https://i.imgur.com/QXUko01.png" width="400">
</div>


# Timeline

![picture 47](https://i.imgur.com/HjTRo7Q.png)  


# Mechanical Assembly

See the suggested list of components below.

<div style="text-align: center;">
  <img src="https://i.imgur.com/bSg7176.png" width="500">
</div>


## Chassis Design

The chassis should be modeled using CAD software. It can be any reasonable size but must fit within the build volume of your 3D printer. For example, the Bambu Lab P1S has a build volume of 256 × 256 × 256 mm. For reference, the chassis shown in this manual measures 205 × 130 × 55 mm.

<div style="text-align: center;">
  <img src="https://i.imgur.com/CSQIYHH.png" width="500">
</div>


<!-- ![picture 64](https://i.imgur.com/qgng56N.png)   -->

## 3D Printing

After designing the CAD of the chassis, save the file as `.stl`. Then slice and 3D print the chassis.


<div style="text-align: center;">
  <img src="https://i.imgur.com/PoovXUC.png" width="500">
</div>

### Bambu Lab P1S

### Ultimaker Cura 
[Ultimaker S5](https://ultimaker.com/learn/the-ultimaker-s5-is-here/) has a build volume (bed size) of 330 x 240 x 300 mm (13 x 9.4 x 11.8 inches)

## Wheel and Motor Mounting

### TODO

<div style="text-align: center;">
  <img src="https://i.imgur.com/qgng56N.png" width="500">
</div>

<!-- <div style="text-align: center;">
  <img src="https://i.imgur.com/eaGLd6G.png" width="500">
</div> -->


## Battery Placement

### TODO

---

# 1. Software Setup
The configuration of Git, GitHub, and SSH and the software environment setup is described. To streamline the development process, we have created a Docker container with Ubuntu 22.04, ROS2 Humble, and dependencies. 

# 1.1 Setting Up Git, GitHub, and SSH

## Install Git

### *Mac*
- Install homebrew and follow the terminal instructions

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- Install git

```bash
brew install git
```

### *Windows*

- Install [Git for Windows](https://gitforwindows.org/), which provides Git Bash (terminal emulator for running Git commands)
  
- Or- install using Windows Powershell
```bash
winget install --id Git.Git -e --source winget
```

- Note: if the above command didn't work, you may need to install [winget](https://chxtio.github.io/ocr_jekyll/) first

```bash
$progressPreference = 'silentlyContinue'
Write-Host "Installing WinGet PowerShell module from PSGallery..."
Install-PackageProvider -Name NuGet -Force | Out-Null
Install-Module -Name Microsoft.WinGet.Client -Force -Repository PSGallery | Out-Null
Write-Host "Using Repair-WinGetPackageManager cmdlet to bootstrap WinGet..."
Repair-WinGetPackageManager
Write-Host "Done."
```

- You can also install Linux for Windows via [WSL (Windows Subsystem for Linux)](https://learn.microsoft.com/en-us/windows/wsl/install)
  - Once setup, Git can be installed using the Linux package manager `apt` below:

### *Ubuntu*

- Install Git

```bash
sudo apt install git
```

## Configure Git
- Configure Git, replacing `"Your name"` and `"your.email@example.com"` with your info (including the quotes) to link your local Git profile with GitHub

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

- Verify configuration
  
```bash
git config --get user.name
git config --get user.email
  ```

## Set up SSH
- Create a new SSH key using your GitHub email as a label

**Note: Press enter to skip through the 3 prompts that follow**

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

- Copy the public key to your GitHub account (See [example](https://github.com/Training-Dummy/howtoforge_git_ubuntu/blob/master/README.md#creating-an-ssh-key))

```bash
cat ~/.ssh/id_ed25519.pub
```

- In GitHub, navigate to [**Settings -> SSH and GPG keys -> New SSH Key**](https://github.com/settings/ssh/new) and paste it there ([example](https://camo.githubusercontent.com/6d19b54f3f16f98804e3b33804d6eb2fa82fb2e796dbce825f8cba2f4b3f74a3/68747470733a2f2f692e696d6775722e636f6d2f676466624a4b6a2e706e67))


- Confirm that your SSH key is connected to your GitHub account

```bash
ssh -T git@github.com
```

- if successful, you should see:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

# 1.2 Recommended Directory Structure

```
~/ocr/
│
├── dev_ws/
│   ├── build/
│   ├── install/
│   ├── log/
│   └── src/
│       └── differential_drive_robot/
│       └── gz_ros2_control/
│
├── ocr-docker/
│   ├── Dockerfile
│   ├── README.md
│   └── docker-compose.yml
│
└── training_ws/
       └── src/
```

## Create Initial Directory Structure

```
~/ocr/
│
├── dev_ws/
│   └── src/
│
├── training_ws/
│   └── src/
```

1\. Create `ocr` folder and cd into it

```bash
mkdir ~/ocr && cd ~/ocr
```

2\. Create the `dev_ws` and `src` folder inside it (ROS packages will be installed in `src` later)

```bash
mkdir -p dev_ws/src
```

3\. Create `training_ws` folder and `src` folder inside it

```bash
mkdir -p training_ws/src
```

4\. Verify that folders have been created inside `ocr`

```bash
ls
```

<!-- Expected output: -->

```output
dev_ws training_ws
```


# 1.3 OCR Docker

<div class="important">
  <strong>Important:</strong> If you have already installed the container, skip to 
  <a href="#step-3-run-the-docker-container">Step 3: Run the docker container</a>.
</div>
<br/>

<!-- > [!IMPORTANT]
> 
> If you have already installed the container, skip to [Step 2: Run the docker container](#step-2-run-the-docker-container). -->



## Step 1: Install the container

- Install and open [Docker Desktop](https://docs.docker.com/desktop/)

- Clone the [repo](https://github.com/oc-robotics/ocr-docker) and cd into it

```bash
cd ~ocr
git clone https://github.com/oc-robotics/ocr-docker.git
cd ocr-docker
```

- Make sure the volume is mounted correctly in `docker-compose.yml`. 
    - The volume `~/ocr/dev_ws/` assumes the following host file structure:

```
~/ocr/
│
├── dev_ws/
│   ├── build/
│   ├── install/
│   ├── log/
│   └── src/
│       └── differential_drive_robot/
│
├── ocr-docker/
│   ├── Dockerfile
│   ├── README.md
│   └── docker-compose.yml
│
└── training_ws/
```

- In your `docker-compose.yml`, the volume should be mounted as:

```
    volumes:
      # - <host_path>:<container_path>
      - ~/ocr/dev_ws/:/ocr/dev_ws/
```

- Pull the base image from Docker Hub

```bash
docker pull mwoodward6/nekton:humble
```
- Build the custom image

```bash
docker build -t ocr-docker:humble .
```

## Step 2: Install any ROS packages 

- As an example, we will install [differential_drive_robot](https://github.com/oc-robotics/differential_drive_robot) in `src`

```bash
cd ~/ocr/dev_ws/src
```

- Clone the repository 

```bash
git clone git@github.com:oc-robotics/differential_drive_robot.git
```


## Step 3: Run the docker container

- cd into `ocr-docker`

```bash
cd ~/ocr/ocr-docker
```

- Start the container in the background (detached mode)

```bash
docker-compose up -d
```

- *Optional*: Open an interactive bash shell inside the container to run commands 

```bash
docker exec -it ocr-humble-nekton-og bash
```

- Browse [http://localhost:6080/](http://localhost:6080/) to access the remote desktop via VNC

![picture 45](https://i.imgur.com/h7OSLJJ.png) 

- Stop the container

```bash
exit # Exit the interactive shell
docker-compose stop
```

- If you need to remove the container

```bash
docker-compose down
```

## Troubleshooting
<!-- ### Fix "ports not available" error -->

- If you encounter an error due to port 6080 being in use, check which processes are using it

```bash
sudo lsof -i :6080
```

- Sample output
  
```
COMMAND    PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
docker-pr  995 root    4u  IPv4  27629      0t0  TCP *:6080 (LISTEN)
docker-pr 1001 root    4u  IPv6  26542      0t0  TCP *:6080 (LISTEN)
```
- Stop the processes

```bash
sudo kill -9 995 1001
```

# 1.4 Differential Drive Robot

## Enter the Docker container
- Inside the Docker container, open a terminal (e.g., run Terminator in NoVNC), and update the GPG key used for the ROS 2 repository

```bash
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

## Install `ros2_control` dependencies

- Install ROS 2 Humble packages required for the [`ros2_control`](https://control.ros.org/rolling/index.html) framework
  - [`ros2_control`](https://github.com/ros-controls/ros2_control): Core control framework for robot hardware interfaces and controllers.
  - [`ros2_controllers`](https://github.com/ros-controls/ros2_controllers): Predefined controllers that can be used to control robot hardware.
  - [`gz_ros2_control`](https://github.com/ros-controls/gz_ros2_control): Integration between ROS 2 control framework and Gazebo from source
    - Note: this will need to be compiled from source (see below)

```bash
sudo apt update
sudo apt install ros-humble-ros2-control ros-humble-ros2-controllers
```

- Install the rosdep rules to resolve Gazebo Garden libraries

```bash
sudo bash -c 'wget https://raw.githubusercontent.com/osrf/osrf-rosdep/master/gz/00-gazebo.list -O /etc/ros/rosdep/sources.list.d/00-gazebo.list'
rosdep update
# check that resolve works
rosdep resolve gz-garden
```

- Compile `gz_ros2_control` from source

```bash
# cd into dev_ws/src
cd src
git clone https://github.com/federicociresola/gz_ros2_control.git -b humble-gz_garden
rosdep install -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO -y
```

- Build the package from the root of the workspace (`dev_ws`)

```bash
cd ..
colcon build --symlink-install
```

- Source the setup

```bash
source install/setup.bash
```

## Launch the Gazebo Simulation
- Run the Gazebo simulation

```bash
ros2 launch differential_drive_robot launch_sim.launch.py
```

![picture 42](https://i.imgur.com/SqxKbpF.png)  

## Visualize with `Rviz`
- Launch `Rviz` with the provided configuration

```bash
rviz2 -d src/differential_drive_robot/config/diff-drive.rviz
```

## Drive the robot with keyboard
- Run `teleop_twist_keyboard` to control the robot
  - Note: is using `ros2_control`, remap the `/cmd_vel` topic to `/diff_cont/cmd_vel_unstamped`

```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard --ros-args -r /cmd_vel:=/diff_cont/cmd_vel_unstamped
```

# 1.5 Raspberry Pi Setup

This setup uses a Raspberry Pi 4. The OS must be configured by flashing the microSD card with Ubuntu 22.04 (see more) and installing ROS2 Humble.

<img src="https://i.imgur.com/xJMgVJ2.png" width="500">

## Setup

- Install [Rapberry Pi Imager](https://www.raspberrypi.com/software/)  
-  Insert the microSD card and choose OS -> other general purpose SO -> **Ubuntu Desktop 22.04 LTS (64-bit)**

- Set up Ubuntu desktop

- Follow the [instructions](https://random-restart.vercel.app/Software-Documentation/ROS/ROS2-Humble-Installation) for installing ROS2 Humble on the Raspberry Pi

- Todo: Set up SSH on the pi for remote connections

## Connecting Peripherals to the Raspberry Pi

<img src="https://i.imgur.com/adBxdjT.png" width="500">

- LCD Screen

    - **Display**: Connect the micro-HDMI port on the Raspberry Pi to the HDMI port on the screen  
    - **Power/touch screen**: Use a micro-USB cable to connect the LCD screen to a USB port on the Raspberry Pi (not just for power, but also for data)

- Raspberry Pi

-    **Power**: Connect the USB-C port on the Raspberry Pi to a power bank or wall outlet.

<img src="https://piportal.digitalharbor.org/cbfe7e712c4ce6e2deed4e129812df9a/rpi-plug-in.gif" width="500">

---

# Electrical Setup

## Software

- Install [Arduino IDE](https://www.arduino.cc/en/software/)

## L293D Motor Driver

- Wire the [circuit](https://www.tinkercad.com/things/ehT2Jv0teTn-l293d-motor-driver?sharecode=ptKgyQ0MTZuHiNs5623u1GnzgUm6TEFuzgF3rDnG1LI) for the motor driver.

![picture 0](https://i.imgur.com/1gINfhA.png)  

- Upload the following `L293D_motor_driver.ino` sketch to the Arduino 

```javascript
// L293D Motor Driver pins for right motor (Motor A)
const int ENA = 11;    // PWM speed control for right motor
const int IN1 = 13;    // Direction control 1 for right motor
const int IN2 = 12;    // Direction control 2 for right motor
 
// L293D Motor Driver pins for left motor (Motor B)
const int ENB = 10;    // PWM speed control for left motor
const int IN3 = 8;     // Direction control 1 for left motor
const int IN4 = 9;     // Direction control 2 for left motor
 
const int switchPin = 7; // Switch to turn robot on/off
 
int motorSpeed = 0; // Starting motor speed
 
void setup() {
    pinMode(switchPin, INPUT_PULLUP);
 
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(ENA, OUTPUT);
 
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
    pinMode(ENB, OUTPUT);
 
    Serial.begin(9600);
    Serial.println("To infinity and beyond!");
    motorSpeed = 255;
    Serial.print("Motor Speed: ");
    Serial.println(motorSpeed);
}
 
void loop() {
    motorSpeed = 255;
    // if (digitalRead(switchPin) == LOW) { // Switch ON (pressed)
    if (digitalRead(switchPin) == HIGH) { // Switch OFF 
        rightMotor(motorSpeed);
        leftMotor(motorSpeed);
    } else { // Switch OFF
        rightMotor(0);
        leftMotor(0);
    }
}
 
void rightMotor(int speed) {
    if (speed > 0) {
        digitalWrite(IN1, HIGH);
        digitalWrite(IN2, LOW);
    } else if (speed < 0) {
        digitalWrite(IN1, LOW);
        digitalWrite(IN2, HIGH);
    } else {
        digitalWrite(IN1, LOW);
        digitalWrite(IN2, LOW);
    }
    analogWrite(ENA, abs(speed));
}
 
void leftMotor(int speed) {
    if (speed > 0) {
        digitalWrite(IN3, HIGH);
        digitalWrite(IN4, LOW);
    } else if (speed < 0) {
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, HIGH);
    } else {
        digitalWrite(IN3, LOW);
        digitalWrite(IN4, LOW);
    }
    analogWrite(ENB, abs(speed));
}
```

## Power calculations

```
8V Battery
 ├──> L293D Vcc2 (motor power)
 ├──> Arduino VIN     (OR buck converter → 5V)
 └──> GND ─────────────┐
                       │
Arduino                │
 ├──> 5V ────> L293D Vcc1 (logic power)
 └──> GND ───────────────┘

```

<iframe 
  src="https://docs.google.com/spreadsheets/d/e/2PACX-1vQC95BsIDwF3d35FrX23txHFuu1lBQMeZXjyyVrMJP-tM-H_xtL_79SU7Kmq02f7_EaCw4Phnupfcjb/pubhtml?gid=1450340132&single=true" 
  width="100%" 
  height="700" 
  style="border: 1px solid #ccc;">
</iframe>

<p style="text-align: center; margin-top: 1rem;">
  <a href="https://docs.google.com/spreadsheets/d/e/2PACX-1vQC95BsIDwF3d35FrX23txHFuu1lBQMeZXjyyVrMJP-tM-H_xtL_79SU7Kmq02f7_EaCw4Phnupfcjb/pubhtml?gid=1450340132&single=true" target="_blank" rel="noopener noreferrer">
    View spreadsheet
  </a>
</p>
