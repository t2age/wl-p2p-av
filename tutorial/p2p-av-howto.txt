WL P2P AUDIO & VIDEO HOWTO
--------------------------

Overview:

a) run the nodejs starter signaling server
b) run the peer B (the guest)
c) run the peer A (the host of audio/video)

This tutorial is basically the same as the WebRTC-Easy-Power tutorial.
There are 2 main differences:
1) This tuto uses normal web browsers to communicate, instead of NodeJS.
2) This tuto does Audio and/or Video instead of data.

The overral connecting procedures are the same.


------------------------------------------------
A) Run the nodejs based starter signaling server
Need to install the "ws" module first:
	npm install ws

Edit the file ws-server-vN.js and adjust to the IP ADDRESS of the machine where it will run.
Change the following line:
	const WEBSOCKET_ADDRESS = "192.168.100.1";

Then, run:
	node ws-server-vN.js

The "N" above is the actual version of the file.


----------------------------------------------
B) Edit and Run the file p2p-av-B-browser.html
Edit this file and change the line:
	const WEBSOCKET_ADDRESS = "192.168.100.1"
	
Then, open the file on your web browser (chromium, firefox, etc)


----------------------------------------------
C) Edit and Run the file p2p-av-A-browser.html
Edit this file and change the line:
	const WEBSOCKET_ADDRESS = "192.168.100.1"
	
Then, open the file on your web browser (chromium, firefox, etc)

-----
DONE!



----------------
FOR RASPBERRY PI
I did the tutorial using a USB WebCam with built-in Microphone, so, before running the html files I had to make the USB WebCam Microphone as the "Default Sound Card".
Click on MENU, then on PREFERENCES, then on AUDIO DEVICE SETTINGS.
Make USB WebCam the default card.


--------------
FIREWALL PORTS
WebRTC uses UDP ports on the ephemeral port range to communicate audio and video, so, I had to open these ports for inbound and outbound. If you are using ufw, then you should do something like these:

	sudo ufw allow out 32768:60999/udp
	sudo ufw allow in 32768:60999/udp

You can find the ephemeral port range with:

	cat /proc/sys/net/ipv4/ip_local_port_range
	
Also, for Chromium web browser I had to open the the port mdns (5353) for outbound, otherwise Chromium refuses the complete the connection...!

	sudo ufw allow out 5353/udp
	

Also, remember that we use TCP port 9000 for the automatic exchange of signals, so need to open for inbound where the server is running, and for outbound where the peers are running.

	sudo ufw allow in 9000/tcp		#on the server
	
	sudo ufw allow out 9000/tcp		#on the peers



-----------
SIMPLE PEER
The tutorial use Simple Peer module (simplepeer.min.js) to create WebRTC connection.
You can get the latest version of the module (file) on the Github SimplePeer repo:

	https://github.com/feross/simple-peer



-----------------
WEBRTC-EASY-POWER
More details can also be found on the webrtc-easy-power tutorial, there are lots in common with this tutorial...

	https://github.com/t2age/webrtc-easy-power

