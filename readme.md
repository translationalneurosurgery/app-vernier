## Verniersl

This is a command-line-interface to collect data from a Godirect device and stream it via labstreaming layer. 

The app is written in python 3.

# Installation


The preferred way is to clone it and install it via pip, e.g by 
```
git clone https://github.com/translationalneurosurgery/app-vernier.git
cd app-vernier
pip install -e .
pip install -r requirements.txt
```
The app wraps  ```pylsl```, and ```godirect``` from Vernier, the latter wraps 
On linux, compilation of the wheels requires libusb and libudev

## Usage

```
usage: __main__.py [-h] [--scan] [--enable ENABLE]
                   [--serial_number SERIAL_NUMBER] [--order_code ORDER_CODE]
                   [--number NUMBER]

Stream Vernier Go-Direct with LSL

optional arguments:
  -h, --help            show this help message and exit
  --scan                report the available devices
  --enable ENABLE       which channels do enable: List
  --serial_number SERIAL_NUMBER
                        The serial number (eg. OK2001B3) of the desired
                        device. Streams are then limited to a single device
  --order_code ORDER_CODE
                        The order code (eg. GDX-ACC for an accelerometer) of
                        the desired device. Can find and stream more than one
                        device
  --number NUMBER       How many devices are expected, aborts otherwise.
                        Helpful as sometimes, one connection might be lost,
                        and we would start streaming then anyways.
```

### Example

The terminology of Go Direct device can be confusing, as the device itself can be called a sensor, while each device has a set of individual sensors which can be turned on or off. Some of them are turned on by default. Check which devices are available, and show their available sensors, and which of there are enabled by default:

```
python -m verniersl --scan
```

Find a Go Direct (C) Acceleration Sensor, enable the default sensors and stream it

```
python -m verniersl --order_code GDX-ACC
```

Find a specific Go Direct (C) Acceleration Sensor, enable the x,y, andz axis acceleration sensors and stream it

```
python -m verniersl --enable "[X-axis acceleration, Y-axis acceleration, Z-axis acceleration]" --order_code GDX-ACC --serial_number 0H101754
```

Find exactly two Hand Dynamometers, enable force sensors and stream them.

```
python -m verniersl --enable Force --order_code GDX-HD --number 2
```




