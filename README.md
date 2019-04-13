# Donkey 2

This is my method to use the Donkey Car, derived from the autorope/donkey2. 

* [Video tutorial.](https://www.youtube.com/watch?v=NGTbzfx7aL4&feature=youtu.be)
* [Video showing how to create a new car with different parts](https://www.youtube.com/watch?v=xqASPxPpkw0&t=91s)

# Starting a fresh Raspbian-Lite installation

1. [Download Raspbian-Stretch-Lite](https://www.raspberrypi.org/downloads/raspbian/)

2. Flash MicroSD card (16-32GB) using your favorite tool.  [balenaEtcher](https://www.balena.io/etcher/) seems to be popular.
3. Configure wireless networking, in the /boot partition create wpa_supplicant file containing:
  ```country=us
   update_config=1
   ctrl_interface=/var/run/wpa_supplicant

   network={
   scan_ssid=1
   ssid="MyNetworkSSID"
   psk="Pa55w0rd1234"
   }
   ```
4.  Enable SSH by creating an empty file in /boot named "ssh"

# Get driving.

Run these commands to setup your donkey car app on your car's raspberry pi.

1. Create and activate your virtual environment.
   ```bash
   virtualenv env --python=python3
   source env/bin/activate
   ```

2. Dowload and install the dependencies for this car template.
   ```bash
   git clone https://github.com/autorope/donkey2.git
   cd donkey2
   pip install -r drive_requirements.txt
   ```
   
3. Run the drive script.
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
