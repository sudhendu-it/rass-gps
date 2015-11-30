Now that we have mobile power and can boot up the pi. We need to add mobile internet access. Fortunately, cell phones have made mobile internet access nearly ubiquitous. To leverage what we already have, we'll be tethering the Raspberry Pi to a cell phone to provide mobile data streaming. If you'd prefer, you can actually perform this project in an `offline` mode where the Python Application will just write data in CSV form to a file on the Pi instead of streaming it. 

### Option 1) Offline Mode

This is an option if you don't want real time tracking or are going through areas with poor cell connection. To do this, just add an `offline=True` constructor parameter to the `Streamer` constructor. By default, it will create a csv file in the directory that the script is being run from. You're constructor will now look like this:

```python
streamer = Streamer(bucket_name="GPS Tracker", ini_file_location="./isstreamer.ini", offline=True)
```

>Note: If you have an Initial State pro tier account, you can then take this file and visualize its data by choosing to upload (or not for privacy) inside the Initial State web application.

### Option 2) Mobile WiFi Tethering

This is the simplest method if you have a smartphone with a data connection and the ability to broadcast a mobile hotspot (like an iPhone or modern Android).

##### iPhone Instructions
1. Open your Settings app
2. Navigate to Personal Hotspot 
3. Ensure toggled on

You will then see a Wi-Fi Password that you can change if you wish.

##### Connecting Raspberry Pi to Mobile Hotspot.

You can do this easily inside the GUI of the Raspberry Pi if you have it connected to a display. You can also do this pretty easily via the commandline with the following steps:

1. `$ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`
2. Add the following into the config:

```
network={
	ssid="iPhone"
	psk="password"
	key_mgmt=WPA-PSK
}
```
> Note: You will need to change the `ssid` to your phones name and the `psk` to the Wi-Fi Password your Personal Hotspot settings shows

Now, when your Personal Hotspot is on and broadcasting over WiFi (make sure your phones WiFi is on as well) then your Raspberry Pi will automatically connect to it if it's on and in range. You can then use the data connection to stream data from the GPS through the Pi to Initial State.

[<< Part 3. Battery Power](8 Part 3. Battery Power)