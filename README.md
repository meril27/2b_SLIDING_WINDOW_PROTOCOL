# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM:

To write a python program for implementation of Sliding window protocol.

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

SERVER:

```
import socket
s = socket.socket()
s.bind(("localhost",9999))
s.listen(1)
print("Server listening...")
conn,addr = s.accept()
print(f"Connected to {addr}")

while True:
    frame = conn.recv(1024).decode()
    if not frame:
       break

    print(f"Received frames: {frame}")
    ack_message = f"ACK for frames: {frame}"
    conn.send(ack_message.encode())

conn.close()
s.close()
```
CLIENT:

```
import socket
c = socket.socket()
c.connect(('localhost',9999))

size = int(input("Enter number of frames to send: "))
l = list(range(size))
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))

i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())

        ack = c.recv(1024).decode()
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s

    break
c.close()
```

## OUPUT

SERVER:

![Screenshot 2025-04-30 234958](https://github.com/user-attachments/assets/5a6d013b-a80b-44ef-a49c-db3d3a21ba67)


CLIENT:

![Screenshot 2025-04-30 235011](https://github.com/user-attachments/assets/797ecca1-1367-4490-a6b0-b80c5418a511)


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
