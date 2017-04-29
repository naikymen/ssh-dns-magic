# Raspberry Pi SSH-based Dynamic DNS Updater

ilovessh

These super raw draft scripts make the pi get its public IP every 10 minutes, and store it on a remote google or AWS server (I used google) when it changes. This Pi-side script must be configured with your server ip and keys. Read it.
The client-side script simply retrieves the public IP from the server, and uses it to connect SSH directly to the pi. The client side script takes arguments for the server IP, server keys, Pi keys and Pi port.
Customize the scripts and/or or use the ~/.ssh/config files on the Pi and Client to make things easier. Put the scripts in /usr/local/bin/ and give them permissions for execution =)

You must setup port-forwarding on your home network, and forward a port of choice to the Pi.

You should add the pi-side script to /usr/local/bin/ or a folder of choice, and update /etc/rc.local accordingly for it to launch at system startup.
nohup /usr/local/bin/getPIP &

You must setup the ssh server on the Pi to accept connections. Instructions for this are widely available on the net, as for all things omitted here.

You should setup the cloud server with a static ip o address, and generate the appropiate RSA keys. You will need 2 of them:
One for client-Pi authentication
One for Pi-server authentication
Make them with ssh-keygen as usual, no passwords this time around.

For mounting the pi on the client machine, sshfs must be installed:
sudo apt-get install sshfs

Note: reverse ssh was an option, but awesome amounts of lag and routing traffic through the google server made this a bad idea, cool though.
