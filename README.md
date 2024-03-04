# Домашнее задание к занятию «Уязвимости и атаки на информационные системы»


---


## Задание 1.


	Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

	Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

	Просканируйте эту виртуальную машину, используя nmap.

	Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

	Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

	Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

	Ответьте на следующие вопросы:

    		Какие сетевые службы в ней разрешены?
    		Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

	Приведите ответ в свободной форме.


## Решение 1


### Какие сетевые службы в ней разрешены?

	21/tcp   open  ftp         vsftpd 2.3.4
	22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
	23/tcp   open  telnet      Linux telnetd
	25/tcp   open  smtp        Postfix smtpd
	53/tcp   open  domain      ISC BIND 9.4.2
	80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
	111/tcp  open  rpcbind     2 (RPC #100000)
	139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
	445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
	512/tcp  open  exec?
	513/tcp  open  login
	514/tcp  open  tcpwrapped
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

### Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)

	1. [vsftpd 2.3.4 - Backdoor Command Execution](https://www.exploit-db.com/exploits/49757)
	2. [Множественные уязвимости в Apache HTTP Server](https://www.securitylab.ru/vulnerability/419165.php)
	3. [ProFTPd 1.3 - 'mod_sql' 'Username' SQL Injection](https://www.exploit-db.com/exploits/32798)


## Задание 2.

	Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

	Запишите сеансы сканирования в Wireshark.

	Ответьте на следующие вопросы:

    		Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
    		Как отвечает сервер?

	Приведите ответ в свободной форме.

## Решение 2.
	
### Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
	SYN
	 Хост с NMAP посылает TCP пакет с флагом SYN и ожидает ответ
	FIN
	 Хост с NMAP посылает TCP пакет с флагом FIN
	Xmas
	 Хост с NMAP посылает TCP пакет с флагами URG, PSH, FIN
	UDP
	 Хост с NMAP посылает пустой UDP заголовок на каждый целевой порт. Так как сканирование происходит очень медленно, примерно один запрос-ответ в секунду

### Как отвечает сервер?
	SYN 
	 Сервер отвечает c akfujv SYN/ASK если порт прослушивается каким либо сервисом, c флагом RST если на порту не запущена никакая служба
	FIN
	 Сервер отвечает с RST флагом, если на порт закрыт, если сервер не отвечает то порт открыт/отфильтрован
	Xmas
	 Сервер отвечает с RST флагом, если на порт закрыт, если сервер не отвечает то порт открыт/отфильтрован
	UDP
	 Сервер отвечает ICMP ответом о недоступности порта, если порт закрыт. Если ответ не получен считается, что порт закрыт
 


---
