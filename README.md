# ESP32-OLED-Fossa-GroundStation for Platformio
Groundstation for the the Fossasat-1 Satellite 

## Supported boards
* **Heltec WiFi LoRa 32 V1** 
* **Heltec WiFi LoRa 32 V2** https://heltec.org/project/wifi-lora-32/
* **TTGO LoRa32 V1** 
* **TTGO LoRa32 V2** 

<p align="center">
<img src="/doc/images/Heltec.jpg" width="300">
</p>

# Quick Install
This project is ready to use with [Platformio](https://platformio.org/). It will take care of all dependencies automatically when building the project. It can also be used with Arduino IDE.

## Platformio (recomended)
Arduino ide instructions bellow.
### Installing platformio
Platformio can be installed as a plugin for many IDEs. You can find a complete list here: https://docs.platformio.org/en/latest/ide.html#desktop-ide

My recommendation is to use VSCode or Atom, you can find installation guides here:

* VSCode: https://docs.platformio.org/en/latest/ide/vscode.html
* Atom: https://docs.platformio.org/en/latest/ide/atom.html

### Open the project in VSCode
Once you have cloned this project to a local directory, you can open it on Visual Studio code in File > Add folder to workspace.

![Add folder to workspace VSCode](/doc/images/add_folder_to_workspace.png "Add folder to workspace VSCode")

Then select the ESP32-OLED-Fossa-GroundStation folder inside the repository and click open.

![Select folder](/doc/images/Select_folder.png "Select folder")

After that, the project should be loaded in visual studio and ready to configure and build.

### Configure the project
First we need to select the board. To do so, open the `Fossa_GroundStation/platformio.ini` file and uncomment one of the lines at the beggining of the file depending on the board you are going to use TTGO ot Heltec.

```
default_envs = 
; Uncomment by deleting ";" in the line below to select the board
;   heltec_wifi_lora_32
;   ttgo-lora32-v1
```

## Build and upload the project
Once the configuration is done, connect the board to the computer and click on the upload button from the platformio toolbar, or go to Terminal -> Run Task -> Upload.

![Upload](/doc/images/upload.png "Upload")

All the dependencies will be downloaded and installed automatically.

Note that if you are a Linux used like me and it is your first time using platformio, you will have to install the udev rules to grant permissions to platformio to upload the progrm to the board. You can follow the instructions here: https://docs.platformio.org/en/latest/faq.html#platformio-udev-rules

## Arduino IDE
You can install the Arduino IDE by downloading it from [arduino.cc](https://www.arduino.cc/en/Main/Software), we recommend the last version, but you should use v1.6 or above.

### Install the Arduino Core for ESP8266
First step is to install support for ESP8266 based boards on the Arduino IDE through the Board Manager. These instruction are copied and adapted from the Arduino Core for ESP8266 documentation here: [https://github.com/esp8266/Arduino/](https://github.com/esp8266/Arduino/).

* Start Arduino and open Preferences window.
* Enter `https://dl.espressif.com/dl/package_esp32_index.json` into *Additional Board Manager URLs* field. You can add multiple URLs, separating them with commas. 
* Open Boards Manager from Tools > Board menu and find *esp8266* platform (and don't forget to select your ESP8266 board from Tools > Board menu after installation).
* Select the version you need from a drop-down box.
* Click *install* button.

Credit to [ESPurna](https://github.com/xoseperez/espurna/wiki/ArduinoIDE) for this section

### Installing dependencies
This project relies on several third party dependencies that must be installed in order to be able to build the binaries you can find the dependencies list below:

* **RadioLib** https://github.com/jgromes/RadioLib
* **ArduinoJson** https://github.com/bblanchon/ArduinoJson
* **ESP8266_SSD1306** https://github.com/ThingPulse/esp8266-oled-ssd1306
* **AsyncTCP** https://github.com/me-no-dev/AsyncTCP.git
* **ESPAsyncWebServer** https://github.com/me-no-dev/ESPAsyncWebServer.git
* **ESPAsyncWiFiManager** https://github.com/alanswx/ESPAsyncWiFiManager.git

### Open the project in Arduino IDE
Once you have cloned this project to a local directory, you can open it from the Arduino IDE in `File > Add folder` to workspace. And select the .ino file which is located in `Fossa_GroundStation > Fossa_GroundStation > Fossa_GroundStation.ino`

![Open on Arduino IDE](/doc/images/open_arduino.png "Open on Arduino IDE")

### Build and upload the project
The next step is to connect the board to the computer, select your board in the board manager of the Arduino IDE `Tools > Boards `

![Select board on Arduino IDE](/doc/images/select_board_arduino.png "Select board on Arduino IDE")

Then select the port where the board is connected to the computer in `Tools > Ports`

And finally click on the rounded arrow button on the top to upload the project to the board or go to `Program > Upload (Ctl+U)`

# Configure Station parameters
The first time the board boot it will generate an AP with the name: FossaGroundStation. Once connected to that network you should be prompted with a web panel to confiure the basic parameters of your station. If that were not the case you can access the web panel using a web browser and going to the url 192.168.4.1.

<p float="left" align="center">
  <img src="/doc/images/config_ap.jpg" width="400" />
  <img src="/doc/images/config_wifimanager.jpg" width="400" /> 
</p>

The parameters that has to be filled are the following:
* **SSID and PASSWORD:** The configuration parameters of you home WiFi AP so that the ground station can connect to internet.
* **STATION NAME:** The name of your ground station. If you have registered yours in the [Fossa Ground Station Database](http://groundstationdatabase.com/database.php), the name should match.
* **LATITUDE and LONGITUDE:** The geographical coordinates of the ground station. This serves the purpose of locating your ground station when you receive a package from the satellite.
* **MQTT_SERVER and MQTT_PORT:** These are the address and port of the MQTT server of the project you should not change them if you want the Ground Station to be able to connect the main server. 
* **MQTT_USER and MQTT_PASS:** These are the credentials of the project MQTT server, the purpose is to be able to collect the most packets from the satellite and manage all groundStations from this central server. You can ask for user and password in this telegram group: https://t.me/joinchat/DmYSElZahiJGwHX6jCzB3Q 
