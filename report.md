# UNIX/Linux operating systems (Basic)

Linux system installation and updates. Administration basics.

## Part 1. Installation of the OS

##### Install Ubuntu 20.04 Server LTS

cat /etc/issue

![cat_etc_issue](img/1.png)

## Part 2. Creating a user

##### Create a user other than the one created during installation. The user must be added to adm group.

Creating a new user

![creating_a_user](img/2.png)

cat /etc/passwd

![cat_etc_passwd](img/3.png)

## Part 3. Setting up OS network

##### Set the machine name as user-1

![set-hostname](img/4.png)

##### Set the time zone corresponding to your current location.

![timedatectl](img/5.png)

##### Output the names of the network interfaces using a console command.

![ip-a](img/6.png)

##### In the report give an explanation for the presence of the lo interface.

Interface lo can be used by network client software to communicate with a server application located on the same computer. That is, if you specify the URL http://127.0.0.1/ or http://localhost/ in the web browser on the computer where the web server is running, it takes you to that computer's web site. This mechanism works without any active connection, so it is useful for testing services without compromising their security as with remote network access.

##### Use the console command to get the ip address of the device you are working on from the DHCP server.

![wget](img/7,0.png)

Decode DHCP in the report.

Dynamic Host Configuration Protocol (DHCP) is a network management protocol used to automate the process of configuring devices on IP networks, thus allowing them to use network services such as DNS, NTP, and any communication protocol based on UDP or TCP. 

##### Define and display the external ip address of the gateway (ip) and the internal IP address of the gateway, aka default ip address (gw)

external IP address
A internal IP address is a range of non-internet facing IP addresses used in an internal network. Internal IP addresses are provided by network devices, such as routers, using network address translation.

![an_external_ip](img/7,1.png)

internal IP address
A internal IP address is a range of non-internet facing IP addresses used in an internal network. Internal IP addresses are provided by network devices, such as routers, using network address translation.

![an_internal_ip](img/8.png)

##### Set static (manually set, not received from DHCP server) ip, gw, dns settings (use public DNS servers, e.g. 1.1.1.1 or 8.8.8.8).

sudo vim /etc/netplan/00-installer-config.yaml

![first](img/9.png)

make some changes

![changed](img/10.png)

after all need to write "sudo netplan apply" to console, then reboot.

##### Reboot the virtual machine. Make sure that the static network settings (ip, gw, dns) correspond to those set in the previous point.

"ping -c 5 ya.ru" to ping 5 times and see the result. Same with 1.1.1.1

![ping_all](img/11.png)

"ip r" to console, to check that our settings was saved.

![ip_r](img/12.png)

## Part4. OS Update

##### Update the system packages to the latest version

"sudo apt update" to download updates.

"sudo apt upgrade" to install updates.


![progress](img/13.png)
upgrade in progress

"sudo apt update" again, to check that all packages are up to date.

![sudo_upgrade](img/14.png)

## Part 5. Using the sudo command

sudo allows a permitted user to execute a command as the superuser or another user, as specified by the security policy. The invoking user's real (not effective) user-ID is used to determine the user name with which to query the security policy.

"sudo usermod -a -G sudo dashilow" to add our user from part-2(dashilow) to sudo group

![sudo_usermod](img/15.png)

"su dashilow" to login as dashilow.

"sudo hostnamectl set-hostname user-1"

![host](img/16.png)

## Part 6. Installing and configuring the time service

"sudo timedatectl set-ntp on" to enable auto-synchronization

![time](img/17.png)

![time2](img/18.png)

## Part 7. Installing and using text editors

##### Install VIM text editor (+ any two others if you like NANO, MCEDIT, JOE etc.)

![vim](img/19.png)
![nano](img/20.png)
![joe](img/21.png)

##### Using each of the three selected editors, create a test_X.txt file, where X is the name of the editor in which the file is created. Write your nickname in it, close the file and save the changes.

![vim1](img/22.png)

:wq to exit with save.

![nano1](img/23.png)

CTRL+s to save, CTRL+x to exit.

![joe1](img/24.png)

CTRL+k+x to exit with save.

![cat](img/25.png)

result

##### Using each of the three selected editors, open the file for editing, edit the file by replacing the nickname with the "21 School 21" string, close the file without saving the changes.

![vim2](img/26.png)

:q! to exit without save

![nano2](img/27.png)

CTRL+x then n to exit w/o save.

![joe2](img/28.png)

CTRL+c then y to exit w/o save.

![cat2](img/29.png)

result

##### Using each of the three selected editors, edit the file again (similar to the previous point) and then master the functions of searching through the contents of a file (a word) and replacing a word with any other one.

VIM:

![vim3](img/30.png)

Before prossing enter:

![vim32](img/31.png)

:s/foo/bar

foo - serching word

bar - replacement word

NANO:

![nano3](img/32.png)

after pressing enter

![nano32](img/33.png)
![nano33](img/34.png)
![nano34](img/35.png)

ctrl+\ to search text u need, then press enter, then enter what you want to paste, then press enter 1 more time, then press y to apply the changes.

JOE:

![joe3](img/36.png)
![jo331](img/37.png)
![joe32](img/38.png)

CTRL+kf to start search, then R to replace, then enter and type new string.

## Part 8. Installing and basic setup of the SSHD service

##### Install the SSHd service.

sudo apt install openssh-server

sudo systemctl enable ssh - to enable ssh on boot

##### Add an auto-start of the service whenever the system boots.

systemctl list-unit-files --type=service --state=enabled

![systemctl](img/39.png)

##### Reset the SSHd service to port 2022.

sudo vim /etc/ssh/sshd_config

![sshd_config](img/40.png)

servise ssh restart

netstat -tan
![netstat](img/41.png)

## Part9. Installing and using the top, htop utilities

##### Install and run the top and htop utilities.

top
![top](img/42.png)

"top - 16:26:52 up 2 min" - uptime
"1 user" - number of authorised users
"load average: 0.00, 0.00, 0.00" - total system load
"Tasks: 102 total" - total number of process
"%Cpu(s): 0.0 us, 0.0 sy, 0.0 nim100.o id" - cpu load
"MiB mem: 1983.4 total, 1516.0 free" - memory load
"2" - pid of the process with the highest memory usage
"160" - pid of the process taking the most CPU time

htop
![htop](img/43.png)

PID
![pid](img/44.png)

PERCENT CPU
![percent_cpu](img/45.png)

PERCENT MEM
![percent_mem](img/46.png)

TIME
![time](img/47.png)

Syslog
![syslog](img/48.png)

## Part 10. Using the fdisk utility

sudo fdisk -l

swapon --show

![fdisk](img/49.png)

## Part 11. Using the df utility

df
![df](img/50.png)
1-K blocks = 1024 bytes.

Size: 9979Mb
Used: 4418Mb
Available: 5032Mb
Use: 47%

df -TH
![df-th](img/51.png)

Size: 9.8Gb
Used: 4.4Gb
Available: 5.0Gb
Use: 47%

## Part 12. Using the du utility

##### Run the du command.

![du](img/52.png)

##### Output the size of the /home, /var, /var/log folders (in bytes, in human readable format).

bytes
![du-shb](img/53.png)

Human-readable
![du-sh](img/54.png)

##### Output the size of all contents in /var/log (not the total, but each nested element using *)

![du_var](img/55.png)

## Part 13. Installing and using the ncdu utility

##### Install the ncdu utility.

sudo apt install ncdu

ncdu

##### Output the size of the /home, /var, /var/log folders.
![ncdu](img/56.png)
![ncdu1](img/57.png)

## Part 14. Working with system logs

vim /var/log/desg

![desg](img/58.png)

vim /var/log/syslog

![syslog](img/59.png)

vim /var/log/auth.log

![auth](img/60.png)

Sep 14 17:00:08, raster7, systemd-logind.

![login](img/61.png)

## Part 15. Using the CRON job scheduler

##### Using the job scheduler, run the uptime command in every 2 minutes.

crontab -e
![crontabe](img/62.png)

vim /var/log/syslog
![crontabe2](img/63.png)

##### Remove all tasks from the job scheduler.
![crontab3](img/64.png)