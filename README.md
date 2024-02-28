# aiyproject-voice
API libraries for AIY Projects (Voice Kit V1 aka Voice HAT)


Burn the latest Raspbian to an SD card

    bookworm

Raspberry Pi Setup


enable i2c and i2s, disable audio  ???
    
    sudo raspi-config
    

    sudo apt update
    sudo apt -y upgrade
    sudo apt install --upgrade python3-setuptools

Setup a virtual environement

    sudo apt install python3.11-venv
    python -m venv env --system-site-packages
    source env/bin/activate

