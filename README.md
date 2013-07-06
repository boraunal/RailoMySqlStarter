RailoMySqlStarter
=================

Apple Script for Starting Railo 4 and MySql Server on MacOS X

How To Use:

Download Start_Railo_MySql.app and Stop_Railo_MySql.app and open it with Apple Automator. Change the paths according to your Railo and MySql installations.

OR

You can just copy and paste following code to Apple Automator:

Start Railo and MySQL
on run {input, parameters}
	tell application "Terminal"
		activate
		do script with command "sudo /Volumes/MyResources/developerRoot/tomcat/bin/startup.command"
		do script with command "sudo /usr/local/mysql/bin/mysqld_safe" in window 1
	end tell
	delay 10
	tell application "System Events"
		if exists process "org.apache.catalina.startup.Bootstrap" then
			tell application "Terminal"
				do script with command "Railo Started Succesifully" in window 1
				set background color of window 1 to {0, 0, 45000, 50000}
			end tell
		else
			display dialog "Railo Failed to Start"
		end if
	end tell
	return input
end run 

Stop Railo and MySQL
on run {input, parameters}
	tell application "Terminal"
		activate
		do script with command "sudo bash /Volumes/MyResources/developerRoot/tomcat/bin/shutdown.sh"
		do script with command "sudo /usr/local/mysql/bin/mysqladmin shutdown" in window 1
	end tell
	return input
end run