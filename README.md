# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
Server.py
```p
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)

print("Waiting for connection...")
conn, addr = s.accept()
print("Connected to", addr)

while True:
    data = conn.recv(1024).decode()

    if not data:
        break

    print("Frames received:", data)

    ack = "ACK for " + data
    conn.send(ack.encode())

conn.close()
```
 Client.py
```p
import socket

s = socket.socket()
s.connect(('localhost', 8000))

n = int(input("Enter number of frames: "))
w = int(input("Enter window size: "))

frames = list(range(1, n+1))
i = 0
```
## OUPUT
### server:
<img width="1917" height="1078" alt="Screenshot 2026-11-03 135312" src="https://github.com/user-attachments/assets/397f7bfa-5863-47be-b773-a5bf83938a35" />

### client:
<img width="1910" height="1077" alt="Screenshot 2026-11-03 135301" src="https://github.com/user-attachments/assets/e69b0a5e-1188-4165-bc1d-059deece67af" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
