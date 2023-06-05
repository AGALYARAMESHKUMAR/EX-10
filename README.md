# APPLICATION USING TCP SOCKETS - FILE TRANSFER PROGRAM
# EXP: 10
# DATE:10-05-2023
# AIM:
To write a python program for creating Chat using TCP Sockets Links.

# ALGORITHM:
# Client:
Import the necessary modules in python
Create a socket connection to using the socket module.
Send message to the client and receive the message from the client using the Socket module in server
Send and receive the message using the send function in socket.
# PROGRAM:
# CLIENT:

import socket
s = socket.socket()
host = socket.gethostname()
port = 60000
s.connect((host, port))
s.send("Hello server!".encode())
with open('received_file', 'wb') as f:
 while True:
  print('receiving data...')
  data = s.recv(1024)
  print('data=%s', (data))
  if not data:
    break
  f.write(data)
f.close()
print('Successfully get the file')
s.close()
print('connection closed')

# SERVER:
import socket

port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)

while True:
    conn, addr = s.accept()
    data = conn.recv(1024)
    print('Server received', repr(data))
    filename = 'myfile.txt'  # Replace 'path/to' with the actual path to the file
    try:
        with open(filename, 'rb') as f:
            l = f.read(1024)
            while l:
                conn.send(l)
                print('Sent', repr(l))
                l = f.read(1024)
        print('Done sending')
    except FileNotFoundError:
        print(f'File {filename} not found.')
    
    conn.send('Thank you for connecting'.encode())
    conn.close()
    
# CLIENT OUTPUT :
![image](https://github.com/AGALYARAMESHKUMAR/EX-10/assets/119394395/2ac18f6b-f78e-45dc-b85b-b8712ceea1df)


# SERVER OUTPUT :
![image](https://github.com/AGALYARAMESHKUMAR/EX-10/assets/119394395/ccda2a5a-845e-49c1-8d68-caab1bb1fc69)


# RESULT:
Thus, the python program for creating File Transfer using TCP Sockets Links was successfully created and executed.
