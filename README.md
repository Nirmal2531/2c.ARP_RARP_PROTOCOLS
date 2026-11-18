# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
```
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('127.0.0.1', 1234))
server.listen(1)

print("ARP Server is waiting...")

conn, addr = server.accept()

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

ip = conn.recv(1024).decode()

mac = arp_table.get(ip, "IP not found")

conn.send(mac.encode())

print("IP Address:", ip)
print("MAC Address:", mac)

conn.close()
server.close()

import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client.connect(('127.0.0.1', 1234))

ip = input("Enter IP Address: ")

client.send(ip.encode())

mac = client.recv(1024).decode()

print("MAC Address:", mac)

client.close()
```
## OUPUT - ARP
<img width="1917" height="1078" alt="Screenshot 2026-11-18 110928" src="https://github.com/user-attachments/assets/c2c4439c-f5b4-4c2b-9b73-f04e8983e25b" />

## PROGRAM - RARP
```
import socket

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind(('127.0.0.1', 1235))
server.listen(1)

print("RARP Server is waiting...")

conn, addr = server.accept()

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

mac = conn.recv(1024).decode()

ip = rarp_table.get(mac, "MAC not found")

conn.send(ip.encode())

print("MAC Address:", mac)
print("IP Address:", ip)

conn.close()
server.close()

import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client.connect(('127.0.0.1', 1235))

mac = input("Enter MAC Address: ")

client.send(mac.encode())

ip = client.recv(1024).decode()

print("IP Address:", ip)

client.close()
```
## OUPUT -RARP
<img width="1917" height="1078" alt="Screenshot 2026-11-18 111215" src="https://github.com/user-attachments/assets/e228f499-5e5c-48c3-a029-1ed4331c5cf7" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
