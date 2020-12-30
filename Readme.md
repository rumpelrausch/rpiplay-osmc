# RPiPlay / deploy

## What's this?

Sync iOS screen to a Raspberry Pi running OSMC.  
It's based upon a fork from https://github.com/FD-/RPiPlay.

## In which environment does it work?

The binary is successfully tested with a Raspberry Pi 3 A+ running
OSMC version 2020.10-1.  
It runs properly in parallel with OSMC as long as there's no video
or audio playing from OSMC.

To circumvent the slow render capabilities it uses the "low latency"
mode of RPiPlay. This may result in occasional loss of video frames
but keeps audio uninterrupted.

The systemd file will run on any systemd-enabled Raspbian derivate, but
the precompiled binary is specifically built for OSMC.

## Prerequisites

- Raspberry Pi attached to a TV/screen via HDMI.
- OSMC  
  The precompiled binary is linked against some OSMC specific libraries.
- Mobile device with iOS version >= 9.
- Both systems have to be connected to the same WiFi.  
  WiFi must allow device-to-device connections (which sometimes is disabled).

## Installation

If your Pi is attached to the internet the easiest way to download
the files is from a shell at the device.  
You could use wget or curl to download files.

1. Download the script `install_libs.sh`  
   - e.g. with wget:  
   `wget https://raw.githubusercontent.com/rumpelrausch/rpiplay-bin/master/install_libs.sh`  
   - sudo run it:  
   `sudo sh ./install_libs`

1. Download the precompiled binary `rpiplay` from the latest release  
   https://github.com/rumpelrausch/rpiplay-bin/releases  
   - Modify it to your liking (change the `NAME` variable).  
   - Sudo copy it:  
   `sudo cp rpiplay.service /etc/systemd/system/`

2. Download the systemd service file.  
   - e.g. with wget:  
   `wget https://raw.githubusercontent.com/rumpelrausch/rpiplay-bin/master/rpiplay.service`  
   - Sudo move it to /usr/local/bin.  
   `sudo mv rpiplay /usr/local/bin`
   - Apply read/execute rights:  
   `sudo chmod a+rx /usr/local/bin/rpiplay`

3. Enable and start the systemd service:  
   `sudo systemctl enable rpiplay`  
   `sudo systemctl start rpiplay`

## Usage

At your iOS device, open the screen sharing dialog (not the instant AirPlay redirection). It should list the `rpiplay` instance with the name you assigned
within the systemd service file. Tap that name, and after a few seconds your
TV should show the iPhone / iPad screen.