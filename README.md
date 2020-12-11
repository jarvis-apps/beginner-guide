# Beginner Guide

An App provides an extension for the Jarvis application and needs to follow a few guidelines



# Contents

- [Important Directories/Files](#important-directoriesfiles)
	- [`app.json`](#appjson)
	- [`setup.py`](#setuppy)
	- [`README.md`](#readmemd)
	- [`*.log`](#log)
- [Communication/MQTT](#communicationmqtt)
- [Web Extensions](#web-extensions)


## Important Directories/Files

```
|-- logs/
|   |-- *.log
|-- system/
|   |-- app.json
|   |-- setup.py
|-- README.md
```
<br>
<br>



### `app.json`

The `./storage/app.json` file contains important information about the app.  
It has to contain at least the following keys:
```json
{
	"name": "App Name",
	"script": "python3 script.py --arguments"
}
```
The Jarvis daemon will fetch your `app.json` file and execute the given script.
<br>
<br>



### `setup.py`

The `./storage/setup.py` file contains installation instructions.  
Use this script to install dependencies (via apt, pip, etc...), modify config files, etc...  
This script is called whenever the user installs your app (inside the script you have root privileges). 
<br>
<br>



### `README.md`

The `./README.md` files contains a short overview over your app, features and how to use it.
<br>
<br>



### `*.log`

The `./log` directory should contain logs for your application. You can keep more log files and they don't have to follow any specific naming scheme but they have to end with .log
<br>
<br>



## Communication/MQTT

Apps can communicate with the Jarvis daemon and other apps via MQTT.  
The MQTT host and port are `mqtt://localhost:2022`

Use the following naming scheme:  
```jarvis/app/<yourappname>```

All MQTT requests are logged by the Jarvis daemon
<br>
<br>



## Web Extensions

TBD

