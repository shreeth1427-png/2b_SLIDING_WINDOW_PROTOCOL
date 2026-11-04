# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
TO IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## SERVER
```
import socket
import json

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

server.bind(('localhost', 1234))
server.listen(1)

print("Server is waiting for client...")

conn, addr = server.accept()

print("Client connected:", addr)

reader = conn.makefile("r", encoding="utf-8")

while True:
    data = reader.readline()

    if not data:
        break

    packet = json.loads(data)
    frames = packet["frames"]

    print("Received frames:", frames)

    conn.sendall("Acknowledgement received from the server\n".encode())

    print("ACK sent to client")

conn.close()
server.close()
```
## CLIENT
```
import socket
import json

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client.connect(('localhost', 1234))

print("Connected to server")

total = int(input("Enter number of frames to send: "))

window = int(input("Enter Window Size: "))

if total <= 0 or window <= 0:
    print("Enter positive numbers")
    client.close()
    exit()

frames = list(range(1, total + 1))

reader = client.makefile("r", encoding="utf-8")

start = 0

while start < len(frames):

    end = min(start + window, len(frames))

    batch = frames[start:end]

    print("Sending frames:", batch)

    message = json.dumps({"frames": batch}) + "\n"

    client.sendall(message.encode())

    ack = reader.readline().strip()

    print("Server:", ack)

    start = end

client.close()
```
## OUPUT
<img width="1600" height="900" alt="WhatsApp Image 2026-11-04 at 8 31 01 AM" src="https://github.com/user-attachments/assets/f422e2c1-3d67-4aa2-85d4-2db3f4f12148" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
