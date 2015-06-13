# checkWan
For router ping the 8.8.8.8 make sure the network is still alive


#!/bin/sh

# The IP for the server you wish to ping (8.8.8.8 is a public Google DNS server)
SERVER=8.8.8.8

# Only send two pings, sending output to /dev/null
ping -c3 ${SERVER} > /dev/null

# If the return code from ping ($?) is not 0 (meaning there was an error)
if [ $? != 0 ]
then
    # Restart the WAN
    logger "WAN ping failed!"
    sleep 3;
    /sbin/reboot
else
    logger "WAN ping successful!"
fi
