### How do configure wheresmypi
[wheresmypi](https://wheresmypi.herokuapp.com/) is a service for finding devices 
on networks that have discovery disabled. This repo contains files for creating
a systemd service on the Raspberry pi that will periodically update it's ip 
address to the wheresmypi service.

Copy `update-ip` and `update-ip.service` to the pi.  Edit `update-ip`.  Change
NAME as desired.  Here is an example:
```
NAME="First%20Build%20Pi"
```
This will create the name "First Build Pi" in the wheresmypi service.  The "%20"
in the name is a space and is required instead of a space.

The following will create the name "First Build Pi 123456":
```
NAME="First%20Build%20Pi$CODE"
```
$CODE will be replaced with last 6 hex digits of the ethernet MAC address.  This
serves to uniquely identify a pi on your network.

Then, move them to the right locations:
```
sudo mv update-ip /usr/local/bin/
sudo mv update-ip.service /lib/systemd/system/
```

Then enable and start the service:
```
sudo systemctl daemon-reload
sudo systemctl enable update-ip
sudo systemctl start update-ip
```

The service is now started and you should see the device on wheresmypi.



