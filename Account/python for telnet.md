# python for telnet script to be pasted into a file
import telnetlib
import time

HOST = "192.168.10.21"
password = "RLD"

tn = telnetlib.Telnet(HOST, timeout=5)

time.sleep(1)
print(tn.read_very_eager().decode())

# Send login password
tn.write(password.encode('ascii') + b"\n")
time.sleep(1)
print(tn.read_very_eager().decode())

# Enter enable
tn.write(b"enable\n")
time.sleep(1)
print(tn.read_very_eager().decode())

# Send enable password (if same)
tn.write(password.encode('ascii') + b"\n")
time.sleep(1)
print(tn.read_very_eager().decode())

# Exit
tn.write(b"exit\n")
time.sleep(1)
print(tn.read_very_eager().decode())

tn.close()






## Creat the file to paste above code into
nano telnet1.py

# run the file
python3 telnet1.py