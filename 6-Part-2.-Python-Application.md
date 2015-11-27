We'll work through utilizing two python libraries to achieve our goal: `pynmea2` and `ISStreamer`

###1. Getting Started

Create or navitage to a directory to store your code:

```
$ mkdir pi-tracker
$ cd pi-tracker
$ nano app.py
```

Inside app.py we'll start with the following most basic python:

```python
import serial
import pynmea2

serialStream = serial.Serial("/dev/ttyAMA0", 9600, timeout=0.5)

while True:
	sentence = serialStream.readline()
	if sentence.find('GGA') > 0:
		data = pynmea2.parse(sentence)
		print "{time}: {lat},{lon}".format(time=data.timestamp,lat=data.latitude,lon=data.longitude)
```

###2. Code Explination

#####1. imports
Importing the `serial` and `pynmea2` modules

```python
import serial
import pynmea2
```

#####2. serial factory
Creating a serial stream on UART at `/dev/ttyAMA0` at `9600` baudrate with a timeout of `0.5` seconds. 

```python
serialStream = serial.Serial("/dev/ttyAMA0", 9600, timeout=0.5)
```

#####3. read from serial
Read the NMEA sentence from serial, parse and check to see if it's a `GPGGA` sentence (which means it will have coordinate data in it), and print the data to the screen.

```python
while True:
	sentence = serialStream.readline()
	if sentence.find('GGA') > 0:
		data = pynmea2.parse(sentence)
		print "{time}: {lat},{lon}".format(time=data.timestamp,lat=data.latitude,lon=data.longitude)
```

[<< Part 2. Application Development](5 Part 2. Application Development) - [Part 2. Data Streaming >>](7 Part 2. Data Streaming)
