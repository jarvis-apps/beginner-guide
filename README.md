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
|-- web-extension/
|   |-- config.json
|   |-- extension-script.php/.html
|-- README.md
```
<br>


### `README.md`

The `./README.md` files contains a short overview over your app, features and how to use it.
<br>
<br>


### `system/app.json`

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


### `system/setup.py`

The `./storage/setup.py` file contains installation instructions.  
Use this script to install dependencies (via apt, pip, etc...), modify config files, etc...  
This script is called whenever the user installs your app (inside the script you have root privileges). 
<br>
<br>


### `logs/*.log`

The `./log` directory should contain logs for your application. You can keep more log files and they don't have to follow any specific naming scheme but they have to end with .log
<br>
<br>


### `web-extension/config.json`

If you want to use a web-extension make sure to create the `web-extension` directory and configure it with the config.json file:
```json
{
	"path": "/bluetooth",	// the browser path for your script (should be the file parameter without .php or .html)
	"material_icon": "bluetooth",	// name of the material icon for the nav bar (take from https://material.io/resources/icons/?style=round)
	"file": "bluetooth.php",	// the name of file in your web-extension directory
	"name": "Bluetooth"	// the name of your extension (will be displayed on the navbar)
}
```
<br>
<br>


### `web-extension/extension-script.php/html`

This file should contain code for your extension. Every file extension is possible, php code will be interpreted only in .php files.

Please make sure you follow these guidelines:  

#### Include scripts  
Your file must start with something like that:
```php
<?php
// functions here

$title = "Document Title";
require "extension.php";
?>
``` 

#### Define a header  
Place a `h1` tag containing an `i` (for icons) tag right after the php code:

```php
<?php /* php stuff */ ?>
<h1><i>bluetooth</i> This is a bluetooth extension</h1>
```

#### Application body  
Place all your other html contents into an application tag.  
If you want to use scripts or styles, insert them after the application tag.

```php
<?php /* php stuff */ ?>
<h1><i>bluetooth</i> This is a bluetooth extension</h1>

<application></application>

<script>
/*
The following functions are already available:
HTTP:
get(url).then(data).catch()					// for get requests
post(url, jsonObject).then(data).catch()	// for post requests
postToUrl(url, jsonObject, method="POST")	// executes a form request
getParam(p)		// extract an url parameter (?x=1&y=2 -> getParam("y") == 2)

Alerts:
launchAlert(callback, title, text, cancelText="Cancel", okText="Ok")
launchInput(callback, title, placeholder, cancelText="Cancel", okText="Ok", passwd=false)
launchFileInput(callback, title, placeholder, formAction=undefined, cancelText="Cancel", okText="Ok")
launchSelection(callback, title, placeholder, options, cancelText="Cancel", okText="Ok")
*/
</script>

<style>
/* a lot of Jarvis styles, colors and layouts are already defined, but you can also add something here */
</style>
```


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

