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
   
## PROGRAM - ARP
## Server.py - ARP:
```python
import socket

s = socket.socket()

s.bind(('localhost', 8000))

s.listen(5)

c, addr = s.accept()

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:

    ip = c.recv(1024).decode()

    try:
        c.send(address[ip].encode())

    except KeyError:
        c.send("Not Found".encode())

```
## Client.py - ARP:
```python
import socket

s = socket.socket()

s.connect(('localhost', 8000))

while True:

    ip = input("Enter Logical Address : ")

    s.send(ip.encode())

    print("MAC Address :", s.recv(1024).decode())

```

## OUTPUT - ARP
## Server.py - ARP:

<img width="1853" height="523" alt="server" src="https://github.com/user-attachments/assets/be543e06-9e46-4a62-829c-81913fa1a708" />

## Client.py - ARP:

<img width="1853" height="520" alt="client" src="https://github.com/user-attachments/assets/4810a23c-82cb-48b3-adb8-3afef84825e5" />



## PROGRAM - RARP
## Server.py - RARP:
```python
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Waiting for connection...")
c, addr = s.accept()
print("Connected to", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:
        break
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
s.close()

```

## Client.py - RARP:
```python
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    ip = input("Enter MAC Address : ")
    if ip == "exit":
        break
    s.send(ip.encode())
    print("Logical Address :", s.recv(1024).decode())
s.close()

```

## OUTPUT -RARP
## Server.py - RARP:

<img width="1855" height="520" alt="server" src="https://github.com/user-attachments/assets/d561172a-9383-43d0-9805-2173f3438a6f" />

## Client.py - RARP:

<img width="1848" height="512" alt="client" src="https://github.com/user-attachments/assets/b252f3fd-dab3-4470-84b2-96b8c7151260" />



## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
