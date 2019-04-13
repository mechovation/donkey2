# Donkey 2

This is my method to use the Donkey Car, derived from the autorope/donkey2. 

* [Video tutorial.](https://www.youtube.com/watch?v=NGTbzfx7aL4&feature=youtu.be)
* [Video showing how to create a new car with different parts](https://www.youtube.com/watch?v=xqASPxPpkw0&t=91s)

# Starting a fresh Raspbian-Lite installation

1. [Download Raspbian-Stretch-Lite](https://www.raspberrypi.org/downloads/raspbian/)

2. Flash MicroSD card (16-32GB) using your favorite tool.  [balenaEtcher](https://www.balena.io/etcher/) seems to be popular.
3. Configure wireless networking, in the /boot partition create wpa_supplicant.conf file containing:
 ```bash
 country=us
 update_config=1
 ctrl_interface=/var/run/wpa_supplicant

 network={
 scan_ssid=1
 ssid="MyNetworkSSID"
 psk="Pa55w0rd1234"
 }
 ```
4.  Enable SSH by creating an empty file in /boot named "ssh"
5. First boot, ssh to your Pi, user:pi password:raspberry  (Need more newbie help here?)
6. Run raspi-config as super user
```bash 
sudo raspi-config
```
* Change hostname
* Change password
* Interface Options
  * Enable Camera
  * Enable I2C
* Advanced: Expand Partition
* Finish & Reboot
```bash
sudo shutdown -r now
```
7. Package Updates
```bash
sudo apt update
sudo apt upgrade
```
8. Install Prerequisites  (possibly more than required??)
```bash
sudo apt-get install git
sudo apt-get install python3 python3-pip python3-virtualenv python3-dev virtualenv
sudo apt-get install build-essential gfortran libhdf5-dev
```

# Installing Donkey 2.

Run these commands to setup your donkey car app on your car's raspberry pi.

1. Create and activate your virtual environment.
   ```bash
   virtualenv env --python=python3
   source env/bin/activate
   ```

2. Dowload and install the dependencies for this car template.  (This can take a LONG time . . . . )
   ```bash
   git clone https://github.com/autorope/donkey2.git
   cd donkey2
   pip install -r drive_requirements.txt
   ```
3.  Activate virtual environment on login.  Add this as the last line of your .bashrc file in your home directory
```bash
source env/bin/activate
```

# Setup RC Controller

We will be using a Arduino Pro Micro to emulate the PS3 joystick.  This will allow the use of the RC transmitter that came with your car during training.  More details to come.

* [ArduinoJoystickLibrary]https://github.com/MHeironimus/ArduinoJoystickLibrary
* [DonkeyPart PS3/PS4 Game Controller]https://github.com/autorope/donkeypart_ps3_controller
* Don't worry about any of the Bluetooth stuff, not using it.
* Steering will be on Axis 0 and Throttle on Axis 4
* We will be editing drive.py and conf.py 

# Get Driving 
   
1. SSH to your Pi:
2. Run the drive script.
   ```bash 
   python drive.py
   ```

# Train an autopilot.

Here are the steps to train an autopilot on your computer after you've transfered the
the tubs from your car's pi to your laptop. 


1. Create and activate your virtual environment.
   ```bash
   virtualenv env --python=python3
   source env/bin/activate
   ```

2. Dowload and install the dependencies for this car template.
   ```bash
   git clone https://github.com/autorope/donkey2.git
   cd donkey2
   pip install -r train_requirements.txt
   ```

3. Train an autopilot
   ```bash
    python train.py /path/to/folder/with/tubs/*
    ```
