# auto-update-dns
Instructions to set a remote connection for Raspberry Pi with auto-updating DNS.

To set up a remote connection to the Raspberry Pi on Raspbian over the network the Pi is in, all that needs to be done is to enable SSH on the Pi and use the Pi's IP address to log in from another computer.

To set up a remote connection from outside the network there's a bit more work to be done.
The following instruction show how I have achived that on my Raspberry Pi 4.

1. Start with signing up or logging in if you already have an account to http://noip.com.
2. Create a hostname and assign the extrernal IP to it.
3. Log in to the Pi either directly or through SSH.
4. Start running the following commands:
    * $ sudo bash (Gets fulls access)
    * $ cd /usr/local/src/ (Navigates to directory)
    * $ wget http://www.no-ip.com/client/linux/noip-duc-linux.tar.gz (Download file)
    * $ tar xf noip-duc-linux.tar.gz (Extracts file)
    * $ cd noip-2.1.9-1/ (Navigates to directory)
    * $ make install (Installs the file)
    * Enter NoIP username
    * Enter NoIP password
    * Reply y or n for all hostnames to be updated
    * Enter time interval in minutes
    * Enter y or n for executing another script
    * $ sudo nano /etc/rc.local (Edit file so it can start when Pi boots up)
    * Inside the file, above the "exit 0" line, add the following: /usr/local/bin/noip2
    * Save file
    * $ sudo /usr/local/bin/noip2 (Starts the service)
    * $ sudo /usr/local/bin/noip2 -s (Checks service status. If all hostnames come up then it's working)
 5. Log in to the router's setup page
    * In the DHCP Reservation page, add the Raspberry Pi and it's internal IP Adress
    * In the Port Forwarding page add the Raspberry Pi and set the port number for remote connection which is 22. (The port number can be changed for security reasons.)
 6. Test the connection by starting PuTTY and log in with the hostname created from NpIP, the Pi's username and password.

That's it! The Pi should be able to be accessed from outside the network.
