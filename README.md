# socat-echo-server
Simple socat echo server to help scanning for open ports/ firewall rules.

## Requirements

Socat is required to run this script. Normally you can install it with the package manager of your choice. 
In my case thats yum:

```
$ yum install -y socat
```

## Usage
The general syntax of this script is `$ ./start-socat <START_PORT> <END_PORT>`.


On your remote server run this command in nmap to perform the port scan:
```
$ nmap -p <START_PORT>-<END_PORT> -v <TARGET_IP>
```

After your scan you should kill all socat processes. This can be done by using `pkill`:
`pkill -e socat` will kill socat instances. This may take a few minutes and will cause heavy load on your machine (even more than starting all the processes, don't know why).

## Limitation

Depending on your hardware you should not start too many instances of the script at once.
To prevent overlead you can only start a maximum of 10,000 socat processes at once.

For my tests I started in sum 20,000 processes in two batches, then performed a scan on this range, killed all socat processes.
Using this technique you will have all ports scanned in around 15 minutes.
