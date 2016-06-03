---
layout: post
title: NodeMcu Set Up on Mac OS
excerpt: "How to start a project with NodeMcu in Mac Environment"
categories: Lua NodeMcu Mac
comments: true
---

#### Install Linux Flasher Tool
```
 pip install esptool
```
[More info](https://github.com/themadinventor/esptool).

#### Download the Latest Version of NodeMcu
Get a custom build from [here](http://nodemcu-build.com/index.php)


#### Install CH340G Driver for Flashing the board
The driver can be downloaded from this [link](http://www.codenuke.net/2015/01/nodemcu-install-ch340-usb-to-serial-for-yosemite.html)

Once the driver is properly installed, you can connect the board to a USB port
on mac. Then find out the serial port name by running cmd ``` ls -l /dev/tty.* ```

The connected port showed up as /dev/tty.wchusbserial1420

#### Flash the Downloaded NodeMcu Image to the Board
Use esptool.py to flash the binary onto the board.

```
# Command is written in this format
esptool.py --port <USB SERIAL PORT NAME> write_flash -fm dio -fs 32m 0x00000 <image_name>.bin

# For example
esptool.py --port /dev/tty.wchusbserial1420 write_flash -fm dio -fs 32m 0x00000 nodemcu-master-7-modules-2016-06-03-01-44-33-float.bin
```

#### Communicate to the Broad through Serial Communication

```
screen /dev/tty.wchusbserial1420 9600
```

You should see the NodeMcu's lua prompt upon successful connection.
Adafruit has a good [tutorial](https://learn.adafruit.com/adafruit-huzzah-esp8266-breakout/using-nodemcu-lua) for setting up the connection with
local wifi.

To scan the local wifi networks:

```lua
-- print ap list
function listap(t)
      for k,v in pairs(t) do
        print(k.." : "..v)
      end
end
wifi.sta.getap(listap)
```

To establish connection:

```lua
wifi.sta.config("accesspointname","yourpassword")
wifi.sta.connect()
tmr.delay(1000000)   -- wait 1,000,000 us = 1 second
print(wifi.sta.status())
print(wifi.sta.getip())
```

exit screen by typing ```ctrl + a``` then ```ctrl + /```

#### Upload Files Using ESPlorer
[ESPlorer](https://github.com/4refr0nt/ESPlorer) is the first IDE listed on NodeMcu's official [document](http://nodemcu.readthedocs.io/en/dev/en/upload/). Once
you downloaded the binary, you can start the IDE by first cd into
the ESPlorer folder, then run ``` java -jar "ESPlorer.jar" ```

#### Conclusion
After playing around with Lua commands for 30min or so, I realized
that before I can implement real IoT applications, I have to getting through a steep learning curve. 
