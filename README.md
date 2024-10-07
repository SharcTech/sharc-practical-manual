# SHARC Practical Manual

The SHARC universal IoT sensor adapter is the quickest method of capturing industrial sensor observations.  With JSON and MQTT native output, the SHARC is ready to transmit data to any networked application within minutes.

This manual will teach you how to:
* select an industrial sensor
* configure your SHARC
* install sensor and capture data
* transmit sensor data to a MQTT server
* interact with the SHARC over MQTT

## Sensor Selection

Industrial sensors can be divided into discrete and analog. A discrete sensor can have two states, on or off.  An analog sensor value is represented across a range of values, such as one volt, one and a half volts, two volts, and so on.  Industrial sensors are powered with 24 volts DC typically have a M12 barrel connector where pin 1 is positive, pin 3 is negative or ground, and pin 4 is the signal.  In a case where a sensor supports multiple types of outputs, pin 2 is used for the secondary signal.  An example of this is a discrete sensor that can be configured as a PNP or NPN circuit.  Another example is an analog sensor where the secondary signal is an alarm when some measurement threshold is crossed.

![sensor types](./images/sensors.png)

The SHARC supports four different sensor types:
* discrete PNP
* discrete NPN
* analog 0-10V
* analog 4-20mA

Lets review the utility and purpose of several different sensors.

### Part Presence and Detection

The Banner Engineering QX4 laser sensor is a highly configurable  discrete sensor with both PNP and NPN circuits.  It is ideal for counting material moving through a process to determine part counts, throughput, and utilization.  Other sensors, such as proximity sensor or inductive ring sensor can be used where practical. 

### Rotational Speed of a Machine Component

An encoder can be placed on the end of a shaft or attached to a wheel to measure the rotational speed of a machine component or the speed at which material is moving through a process.  An encoder resolution determines how many ‘ticks’ there are in a single rotation.  Each discrete ‘tick’ is a signal detected by the SHARC, which can detect signals up to 9kHz or 9000 per second.

### Operating State of a Machine Component

Many machine components operate on AC power.  Using an analog current transformer (CT) sensor we can measure the amperage flowing through a power circuit.  As an example, we can place a CT sensor on laser power source to determine the on time of a laser cutter.  When the laser cutter is running it will draw some current.  By setting a threshold we can capture the times at which the laser starts and stops.

### Direct Observation of Temperature or Pressure

Other important process variables might include temperature or air and hydraulic pressure.  Using the appropriate analog sensor we can directly observe the process variable over time.

## SHARC Configuration

You can think of the SHARC as an adapter, just like the ones you might use at home to convert a USB to an HDMI signal.  The M12 barrel connector of the SHARC accepts an industrial sensor.  The  RJ35 network connector of the SHARC provides network communications to both configure the device and retrieve sensor  readings.  The four position rotary switch determines which sensor circuit is active.  If you are connecting a PNP sensor, set the rotary switch to position zero.  If you are connecting a 4-20mA sensor, set the rotary switch to position three.

Both the SHARC and sensor require power.  There are two options for power delivery.  The first option is to use Power-over-Ethernet.  The second option is to use a Y-cable or T-adapter and provide power over the M12 barrel connector.  The second option is practical when WIFI wireless transmission is possible and 24VDC can be diverted from the machine’s power.

Connect the sensor and SHARC together using the provided five pin M12 cable.  Pin four is always the signal wire.  Pins one and three are the power pins.  In some cases a field wireable connector must be used to provide the correct pin configuration.

Plug the PoE network cable into the SHARC.  This will power on the SHARC and the sensor.  While booting, the LED light will remain yellow.  Once booted the light will change to red and green for MQTT network mode or cyan and blue for Bluetooth mode.  Let’s configure the SHARC using Bluetooth.  For this we will either use the SharcStudio iOS app or our Chrome browser on a computer with Bluetooth.  To get the SHARC into Bluetooth mode, hold down the user button until the device reboots, then release the button.  You are in Bluetooth mode when the LED turns cyan color.  You are now ready to establish a connection to the SHARC.

Open your Chrome browser and navigate to https://sharc.tech.  From there select BLE and scan for devices.  Once your device is found, select Pair and wait for the browser to pull the device’s configuration.

### Device Information

### Network Configuration

### Sensor Configuration

### Live Sensor Data

## MQTT Transmission

MQTT is a popular communication protocol across Industry 4.0.  It is light weight and offers a publish and subscribe mechanism well suited for reporting data by exception.  A server or MQTT broker is required as the centerpiece of the deployment.  Each SHARC is an MQTT client to the broker.  The SHARC subscribes to specific topics as channels to configure and interface with the SHARC.  The SHARC also publishes its data to specific topics as channels to get the data out of the device.

### Install an MQTT Broker

We will install the open-source Mosquitto broker on our Windows machine.  Download and install Mosquitto broker from https://mosquitto.org/files/binary/win64/mosquitto-2.0.19-install-windows-x64.exe.  The broker will install itself as a Windows Service.

mosquitto_service.png

Next, configure the Windows Firewall to allow inbound traffic on TCP port 1883.

firewall_inbound_rule.png

Finally, modify the broker configuration to allow anonymous connections external to your computer.  Then restart the Mosquitto service.

mosquitto_conf_allow_anon.png

mosquitto_conf_listener.png

mosquitto_service_restart.png

Find your computer’s IP address and test the connection using MQTT Explorer, found here: https://github.com/thomasnordquist/MQTT-Explorer/releases/download/v0.4.0-beta.6/MQTT-Explorer-Setup-0.4.0-beta.6.exe.

ipconfig.png

mqtt_explorer_test.png

mqtt_explorer_test_connected.png

### Point SHARC to Our Broker

### View SHARC Configuration and Sensor Readings
