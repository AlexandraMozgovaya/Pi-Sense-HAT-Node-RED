# Simple Raspberry Pi - weather reporter ( Temp and Humidity )


![Sense HAT image](https://github.com/IBMDeveloperNYC/Pi-Sense-HAT-Node-RED/blob/master/SenseHat-NodeRED-flat.jpg)

## Introduction
In this hands on workshop you will learn 3 things:

### (1) The fundametals of Node-RED

<details><summary><strong>Learn More about Node-RED</strong></summary>
 
```text

Node-RED is:

* Low-code programming tool and framework for event-driven applications
* a Programming tool for wiring together hardware devices (e.g. IoT), APIs and online services in new and interesting ways
* provides a browser-based editor that makes it easy to wire together flows using the wide range of nodes in the palette that can be deployed to its runtime in a single-click.

```

> For in depth information take a look at the [ official Node-RED website https://nodered.org/](https://nodered.org/)

</details>

### (2) How to make a simple home Temerature and Humidty clock that shows local data as well as interacting with Node-RED on the IBM Cloud

### (3) a simple approach to programming the senseHat ( a relatively inexpensive rasberry pi Cape )
<details><summary><strong>Learn More about the SenseHat</strong></summary>
 
 The sense hat is ...
 
 ( a relatively inexpensive rasberry pi Cape )
 
 ```text
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure 
dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non 
proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
```
</details>


## prerequisites
Raspberry Pi 2 or 3 - not sure about v4

[Sense HAT](https://www.adafruit.com/product/2738)

SSD card ( 8 or 16 Gb should be fine )

### The Sense HAT is an add-on board for the Raspberry Pi

The board allows you to make measurements of temperature, humidity, pressure, and orientation, 
and to output information using its built-in LED matrix.

We will use it to publish Temperature(Centigrade) and Humidity metrics to [Node-RED](https://nodered.org/) on the [IBM Cloud](https://cloud.ibm.com) - free account!

It will also display the Temperature(Centigrade) to the matrix screen everytime your `cron` job runs

## These instructions were run on a Raspberry Pi v3 and with the latest version of Raspbian OS 
* Setting up Raspbian on your Pi is easiest with [NOOBS](https://www.raspberrypi.org/documentation/installation/noobs.md)

## setup the Sense HAT
* setting up [Sense HAT](https://projects.raspberrypi.org/en/projects/getting-started-with-the-sense-hat)

## Open or ssh into your pi, then setup a cron job as root on Raspberry Pi with a SenseHat
```sh
#become root user
sudo su
touch /home/pi/sense.log
crontab -e
# add the following line to POST updates every 5 or any interval you like, I chose 5 minutes
echo "5 * * * * /usr/bin/python /home/pi/dev/pi-hat-node-red/push.py >> /home/pi/sense.log 2>&1"
# restart cron
systemctl restart cron

exit
#revert to pi user
mkdir -p /home/pi/dev && cd /home/pi/dev

#clone repo
git clone https://github.com/Grant-Steinfeld/pi-hat-node-red.git
cd pi-hat-node-red
ls
stat push.py
echo "push.py should be here"
```

### copy the contents of Pi-SenseHat-Ingress.Node-RED.json to your clipboard and paste into your node red editor and deploy it.

### Note your NodeRED endpoint POST URL and pass that as the first parameter to  push.py  

```sh
echo "example call"
python3 push.py https://<<yourNodeRedSubDomainname>>.mybluemix.net/<<your-end-point-path>>

#replace the values in the << >> with valid NodeRED path parts"
```

 
