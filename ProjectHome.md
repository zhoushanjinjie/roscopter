ROS interface for Arducopter using Mavlink 1.0 interface.

Currently it supports controlling the arducopter by overriding the RC command, and it publishes all the sensor data.


# Building #
  * Checkout roscopter:
> > ` git clone https://pechkas@code.google.com/p/roscopter/ `
  * Checkout and build mavlink in the roscopter folder, or create a symlink to your existing mavlink build. The `roscopter/mavlink` folder should point to the built mavlink folder.
  * Mavlink can be checked-out from : git clone https://github.com/mavlink/mavlink.git
  * Build roscopter using `rosmake`.


# Running #
```
nodes/roscopter.py --device=/dev/ttyUSB1 --baudrate=57600 
```

  * `--device` specifies the serial device. It could be `/dev/ACMx` or `/dev/ttyUSBx`.
  * `--baudrate` specifies the baudrate. This should be 57600 if you are using XBee to talk to the APM, and 115200 if you are using a direct wired connection.


# Getting sensor data #
Roscopter publishes sensor and other state data on the following topics:

  * /attitude : imu information
  * /gps :gps fix
  * /rc : value of current raw rc input
  * /state : shows wether the copter is armed or not, and the current mode
  * /vfr\_hud : airspeed, groundspeed, heading, throttle, alt, climb

# Control #
To enable control, run the roscopter node with --enable-control=true option.
```
nodes/roscopter.py --device=/dev/ttyUSB1 --baudrate=57600 --enable-control=true
```
Currently the only way of controlling the arducopter is by publishing to `/send_rc` topic. It takes raw RC channel values (between 1000-2000), and uses them to override the values received from the RC controller. To give control back to RC, publish 0 for the corresponding channel.

# Arming/Disarming #
Arming and disarming can be done by calling the `/arm` and `/disarm` services with no parameters.


# Donate #
Your donations will keep me motivated to improve this project:
  * [Paypal](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=A65VGXMBXH9BW&lc=US&item_name=ROSCopter&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donate_SM%2egif%3aNonHosted)