# aiyproject-voice
API libraries for AIY Projects (Voice Kit V1 aka Voice HAT)

Only mic, HP and button/led

1-Install

Burn the latest Raspbian to an SD card

    bookworm

2-Raspberry Pi Setup


enable i2c and i2s, disable audio  ???
    
    sudo raspi-config
    

    sudo apt update
    sudo apt -y upgrade
    sudo apt install --upgrade python3-setuptools

Add the AIY Debian packages repo
Add AIY package repo:

    echo "deb https://packages.cloud.google.com/apt aiyprojects-stable main" | sudo tee /etc/apt/sources.list.d/aiyprojects.list

Add Google package keys:

    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
    
Update and install the latest system updates (including kernel):

    sudo apt-get update
    sudo apt-get upgrade


3-Setup environement

virtual environement
https://learn.adafruit.com/python-virtual-environment-usage-on-raspberry-pi

    sudo apt install python3.11-venv
    python -m venv env --system-site-packages
    source env/bin/activate

Install the AIY Projects Python library

    sudo apt-get install -y git
    
clone this aiyprojects-raspbian repo from GitHub:

    git clone https://github.com/mchambon/aiyprojects-raspbian.git AIY-projects-python

And now install the Python library in editable mode:

    sudo pip3 install -e AIY-projects-python


4-Install Voice HAT packages

Voice HAT does not require any driver installation. You only need to load device tree overlay on boot:

    echo "dtoverlay=googlevoicehat-soundcard" | sudo tee -a /boot/firmware/config.txt

Disable built-in audio:

    sudo sed -i -e "s/^dtparam=audio=on/#\0/" /boot/firmware/config.txt

Install PulseAudio:

    sudo apt-get install -y pulseaudio
    sudo mkdir -p /etc/pulse/daemon.conf.d/
    echo "default-sample-rate = 48000" | sudo tee /etc/pulse/daemon.conf.d/aiy.conf

choose pulse audio
    
    raspi-config 
    
You may also need to disable module-suspend-on-idle PulseAudio module for the Voice HAT:

    sudo sed -i -e "s/^load-module module-suspend-on-idle/#load-module module-suspend-on-idle/" /etc/pulse/default.pa
    reboot


5-Test 

Audio output & Mic

    python AIY-projects-python/Checkpoints/check_audio.py

Button    

    python AIY-projects-python/src/exemples/button_led.py
