# ToyPad Emulator for Lego Dimensions

Big thanks to Berny23, I could have never even have started a project like this, without their work this would not exist. Consider donating to them below:
<a href="https://www.buymeacoffee.com/Berny23" title="Donate to this project using Buy Me A Coffee"><img src="https://img.shields.io/badge/buy%20me%20a%20coffee-donate-yellow.svg" alt="Buy Me A Coffee donate button" /></a>
</span>

Allows you to connect an emulated ToyPad to your PC or video-game console.

## Features
- Supports all available characters and vehicles
- Save vehicle upgrades
- Supports most if not all of the consoles the game is available for (please test if you're able)
- Confirmed working on Cemu and real Wii U
- Can be configured easily by following the instructions below

## Demo
![](https://i.imgur.com/iyWVObT.png)

Video for Cemu emulator: https://www.youtube.com/watch?v=7CBa9u2ip-Y

## Prerequisites
* **Raspberry Pi Zero W** ($10) or similar single board computer with Network support
* USB A to micro USB A cable that supports data transmission (e. g. your phone's charging cable)
* 2 GB+ Micro SD card
* Internet connection on your PC and single board computer

## Installation

1. If you're using a Raspberry Pi Zero W, flash Raspberry Pi OS Lite to your SD card using [the Raspberry Pi Imager tool](https://www.raspberrypi.org/software/) and follow [this](https://www.raspberrypi.org/documentation/configuration/wireless/headless.md) as well as [this](https://www.raspberrypi.org/documentation/remote-access/ssh/README.md) instruction for headless installation.

2. Connect your device to your PC via USB cable (don't use the port on the edge of the Pi Zero!).

4. Use SSH to run the following commands:<br>
   ```bash
    echo "dtoverlay=dwc2" | sudo tee -a /boot/config.txt
    echo "dwc2" | sudo tee -a /etc/modules
    echo "libcomposite" | sudo tee -a /etc/modules
    echo "usb_f_rndis" | sudo tee -a /etc/modules
    
    sudo apt install -y git
    git clone https://github.com/Cort1237/LD-ToyPad-Emulator.git
    cd LD-ToyPad-Emulator
    
    sudo cp usb_setup_script.sh /usr/local/bin/toypad_usb_setup.sh
    sudo chmod +x /usr/local/bin/toypad_usb_setup.sh
    (sudo crontab -l 2>/dev/null; echo "@reboot sudo /usr/local/bin/toypad_usb_setup.sh") | sudo crontab -
   ```
   
5. Reboot you device with this command:
   ```bash
    sudo shutdown -r now
   ```
   
6. Connect via SSH again and run the following commands:
   ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
    
    nvm install 11
    sudo setcap cap_net_bind_service=+ep `readlink -f \`which node\``
    
    cd LD-ToyPad-Emulator
    npm install
   ```
   
7. Run the emulator server with this command:
   ```bash
    node index.js
   ```

## Usage
Type your single board computer's IP address in a browser to use the emulator. If you want to turn it off, just use the command from earlier (without -r) to shut the device down via SSH.

Note: Not currently usable on mobile devices.

## Acknowledgements
Shoutout to ags131 for writing one of the main NodeJS libraries I'm using: https://www.npmjs.com/package/node-ld

My project would've been impossible to create without this guy's research.

## License
[MIT](https://choosealicense.com/licenses/mit/)
