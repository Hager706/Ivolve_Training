# Lab 3: Shell Scripting Basics
## Objective
Create a shell script that pings every server in the 172.16.17.x subnet, where x is a number between 0 and 255. The script will display a message indicating whether each server is reachable or unreachable.

## Script Overview
The script ping_servers.sh performs the following tasks:

Iterates through the IP range 172.16.17.0 to 172.16.17.255.

Pings each server with 1 packet and a timeout of 1 second.

Displays a message indicating whether the server is up and running or unreachable.
---

## Steps
1. Create the Script ping_subnet.sh.
```bash
#!/bin/bash

# Loop through the IP range 172.16.17.0 to 172.16.17.255
for ip in 172.16.17.{0..255}; do
ping -c1 ${ip} > /dev/null 2>&1
if [ $? -eq 0 ]; then
  echo "Server $ip is up and running."
else
  echo "Server $ip is unreachable."
fi
done
```
2. Make the Script Executable
```bash
chmod +x ping_servers.sh
```
3. Run the Script
```bash
./ping_servers.sh
```
### output 
![Alt text](Screen2.png)