# Rock4se_config
Configuring Rock4se with Headless settings and other minor documentation.


## Headless install

Used ChatGPT to install drivers for my Armbian 24.8.0 Bookworm system

```
sudo apt update
sudo apt install mesa-utils
sudo apt install -y mesa-vulkan-drivers
sudo apt install xvfb mesa-utils vulkan-tools
```

## 1. Install Xvfb:
`sudo apt install xvfb mesa-utils vulkan-tools`
## 2. Start Xvfb:

`Xvfb :1 -screen 0 1920x1080x24 &`
## 3. Set Display Environment Variable:
`export DISPLAY=:1`

## 4. Verify GPU Installation:
```
glxinfo | grep "OpenGL renderer"
vulkaninfo | grep "GPU id"
```
## 5. Create a Startup Script:
`sudo nano /usr/local/bin/startxvfb.sh`

## 6. Add the Following to the Script:
```
#!/bin/bash
Xvfb :1 -screen 0 1920x1080x24 &
export DISPLAY=:1
```
## 7. Make the Script Executable:

`sudo chmod +x /usr/local/bin/startxvfb.sh`
## 8. Add the Script to Startup:
`sudo crontab -e`
and add:

`@reboot /usr/local/bin/startxvfb.sh`

Using `DISPLAY=:1 glxgears` for example, I can get glxgears running and showing frames per second on the terminal.
DISPLAY=:1 glxgears
