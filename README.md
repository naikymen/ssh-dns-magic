# Raspberry Pi SSH-based Dynamic DNS Updater

ilovessh

These super raw draft scripts make the pi get its public IP every 10 minutes, and store it on a remote google or AWS server (I used google) when it changes. This Pi-side script must be configured with your server ip and keys. Read it. Applications are endless.
The client-side script simply retrieves the public IP from the server, and uses it to connect SSH directly to the pi. The client side script takes arguments for the server IP, server keys, Pi keys and Pi port. The client might be a PC or Android phone.
Customize the scripts and/or or use the ~/.ssh/config files on the Pi and Client to make things easier. For your convenience, put the scripts in /usr/local/bin/ and give them permissions for execution =)

You must setup port-forwarding on your home network, and forward a port of choice to the Pi.

You must install dnsutils on the Pi, i used the dig command: sudo apt-get install dnusutils
You should add the pi-side script to /usr/local/bin/ or a folder of choice, and update /etc/rc.local accordingly for it to launch at system startup.
I added: nohup /usr/local/bin/getPIP &

You must setup the ssh server on the Pi to accept connections.
Instructions for this are widely available on the net, as for all things omitted here.

You should setup the cloud server with a static ip or address, and generate the appropiate RSA keys. You will need 2 of them:
One for client-server authentication (one for each client)
One for Pi-server authentication (just the one)
Make them with ssh-keygen as usual, no passwords this time around. Add the public keys to the authorized_keys file on the cloud server.

For mounting the Pi on the client PC, sshfs must be installed: sudo apt-get install sshfs
Mounting through ssh is awesome!
On Android I've been using Solid Explorer, there may be other/better alternatives.

Note: reverse ssh was an option, but awesome amounts of lag and routing traffic through the google server made this a bad idea, cool though.
