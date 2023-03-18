<h1>Port Scanner</h1>

#!/bin/python3
<br />


import sys
<br />
import socket
<br />
from datetime import datetime
<br />

#define target
<br />
if len(sys.argv) == 2:
<br />
        target = socket.gethostbyname(sys.argv[1]) #translate hostname to ipv4
<br />
else:
<br />
        print("Invalid amount of argument")
<br />
        print("Syntax: python3 scanner.py <ip>")
<br />

#add a pretty banner
<br />
print("." * 50)
<br />
print("Scanning target " +target)
<br />
print("Time started: " +str(datetime.now()))
<br />

try:
<br />
        for port in range(50,85):
<br />
                s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
<br />
                socket.setdefaulttimeout(1)
<br />
                result = s.connect_ex((target,port)) #returns an error indicator
<br />
                if result == 0:
<br />
                        print("Port {} is open".format(port))
<br />
                s.close()
<br />

except KeyboardInterrupt:
<br />
        print("\nExiting program.")
<br />
        sys.exit()
<br />

except socket.gaierror:
<br />
        print("Hostname could not be resolved.")
<br />
        sys.exit()
<br />

except socket.error:
<br />
        print("Couldn't connect to server.")
<br />
        sys.exit()
<br />
