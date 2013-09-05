pkill -f procnamex (kills all processes with name procnamex)
ps aux | grep procnamex (show all processes with name procnamex)
ps -p $$ (displays the current shell that is used)
pstree -a (display a tree of processes with command line arguments)
kill -9 12030 (kills process with PID 12030. -9 sends KILL signal to process so use it only when absolutely necessary)

man -k foo (search foo in man pages descriptions)
man -wK foo (search foo in man pages bodies)
whatis (displays short descript from the manual)

$? (reads the exit status of the last command executed. After a function returns, $? gives the exit status of the last command executed in the function)
$$ (current process PID)
$! (PID of the last backgrounded process)
!! (repeat last command - useful combo - sudo !!)
!$ (last argument of the previous command)
!:n (n-th argument of the previous command)
!n (execute n-th line in history)
!-5 (execute current -5 line in history)
!foo (execute the last foo command in history)

history (show history of all commands in shell) - bash history is written in the file ~/.bash_history
history -c (deletes shell history from RAM)
export HISTTIMEFORMAT="[%F] [%T] " (set the HISTTIMEFORMAT variable so that the history contains date and time for each command - only for current session - add to ~/.bash_profile to make it permanent)
fc (processes command line history - open and editor to modify and reexecute previously entered commands)

sudo update-rc.d foobar defaults (installs the init script foobar for all run levels - foobar script must be in the /etc/init.d/. This will enable to call service foobar start)
sudo update-rc.d foobar start 80 2 3 4 5 . stop 20 S 1 6 (foobar service will be started at sequence 20 in levels 2-5 and stoped at sequence 20 in level S, 1 and 6. On debian 6 if using dependency based boot "insserv" scripts must have LSB headers)

w (who is logged and what they are doing)
last (show listing of last logged in users)
lastlog (reports the most recent login of all users or of a given user)
whoami (shows your username)
id (prints info about user: real / effective userID, groupID etc.)

free -m (display amount of free and used memory in the system -m in MB)
vmstat (display information about processes, memory, paging, block IO, traps, disks and cpu activity)
dmidecode (displays DMI (SMBIOS) - all system information)
iostat (I/O statistics for devices and partitions)
iotop (top-like I/O monitor)
netstat (network statistics tool usefull in analyzing network connections, routing tables, network interfaces)
ifstat (ethernet  traffic monitor)
apachetop -f /var/log/apache2/access.log (displays real-time web server statistics)
dstat (generating system resources - usefull monitor tool)

time foobar (runs foobar and summarizes system resource usage)

sysctl -a (display all kernel parameters at runtime)
lsb_release -a (displays distribution version information)
uname -a (prints more general system information)
lsof (display all open files)
telinit (change system run level)
cat /proc/cpuinfo (display info about cpu)
cat /proc/meminfo (display info about memory)

sudo strace -p 123 (trace system calls and signals for process with PID 123 - usefull when debugging processes. Use -f to trace forked processes and -e to see only file activity - usefull when tracking evasive config files)

fuser (identify processes using files or sockets)
sudo fuser -4 -v -n tcp 80 (find all processes using TCP port 80, -v verbose, -4 - IPv4)

stat foo.txt (display file status - similar to properties on win systems - displays access/modify/change dates and other useful info for the file)
file foo.txt (detect file type; -bi will detect encoding; try to use chardet if cannot detect charset properly)
chardet foo.txt (universal character encoding detector)

top (show linux tasks / processes)
htop (proces monitor)
atop (resource monitor)

tar cvf foo.tar bar/ (creates gzipped tar archive with name foo.tar from the folder bar)
tar xvf foo.tar (extracts gzipped tar in current directory)

sed -i "s/foo/bar/g" bazfile (global inplace search and replace in files - replaces foo with bar in file bazfile)

-----------------
ssh root@hostname.example.com -p 12345 *** OR *** ssh hostaname.example.com -l root -p 12345 (ssh connection on server hostaname.example.com with username root on port 12345)
ssh -L 1234:localhost:2345 user@hostname.example.com (port forwarding - useful when you want to connect on server hostname.example.com on port 2345, from your machine on port 1234 - usefull to connect to restricted services via ssh)
ssh -D 9999 -C foo@bar.example.com (-D application-level port forwarding - usefull when wanting to connect an application through proxy on another server - e.g. connecting with Firefox remotely to an server as it was connected locally)

~/.ssh/config
Host foobar 
	HostName server.example.com
	User foo
	Port 666
	LocalForward 9999 localhost:10000
	IdentityFile ~/.ssh/somkeynames.key
	
ssh -f -N foobar (open local port fowarding: -f execute in background, -N do not execute remote command)

foobar can be anyname you like
LocalForward/IdentityFile is optional
-----------------

sftp root@hostname.example.com  (SFTP connection to remote server)
get Foo.txt (with connected with sftp gets the file Foo.txt from remote server)

sudo su (login as super user)
su - foobar (login as foobar user - but spawn shell in login mode - e.g. bash reads ~/.bash_profile in login mode and ~/.bashrc in nonlogin mode)

chsh -s /bin/bash foobar (change login shell for the foobar user to bash. Normal users can change only their shell, root can change any account)

df -ahT /foo/bar/ (displays file system disk usage and partition types; if path is ommited all mounted disk usage is displayed)
mount (used for mounting filesystem or displaying the mounted filesystem if used without options)

cd .. (go to parent  directory)
cd ~ (go to home directory)
cd - (returns to the previos location)
ls -lah (list directory contents with details)
du -sh (display total folder size)
dig -x 176.9.134.62 (DNS lookup - reverse lookup of IP adress)
mv bla.x foo.x (move - move file to the directory or if the directory is same rename the file)
chmod 777 -R Foo (add all permissions to the folder Foo recursively)
chown administrator foo (set admnistrator user as owner of the file / folder foo)
chgrp administrator foo (set admnistrator user as group of the file / folder foo)
umask 022 (default umask; sets the default permissions on the file when created. The mask is reversed from chmod - eg. umask 777 will mean that the new file will not have ---/000 permission or umask 000 that the new file will have rwx/777 permission)

setfacl/getfacl (get/set file ACL - more advanced version of default file permissions)

touch foo.bar (create file with name foo.bar)
echo "foobar" > foo.bar (creates file foo.bar if does not exists or overwrites existing file and writes foobar inside)
echo "foobar" >> foo.bar (creates file foo.bar if does not exists and writes foobar inside, appends to the file if file already exits)

INSERT (keyboard button) enables editing the file
ESCAPE (keyboard button) enables entering the commands in editor
:q! (command for force exiting without changes)
:wq (save changes and exit)
:$ (go to the end of file)
/ search in file (go to next result with n)

Ctrl+C kills current process 
sh deploy.sh *** OR *** ./deploy.sh (start script)
./deploy.sh & (starts the script as separate process - the terminal can be turned off and the process will still be running)

Ctrl+L (clear the terminal screen)
Arrow up / down (displays the previously used commands)
Shift+Insert (paste)

apt-get install packageNameFoo (installs a packageNameFoo program from the default repository)
apt-get update (resynchronizes package index from their sources - updates versions of the apps in the APT)
apt-get purge packageNameFoo (remove packageNameFoo program and clear configuration files for the package)

apt-cache show packageNameFoo (displays detailed info about current and installed package)
apt-cache policy packageNameFoo (displays only verision info about current and installed package)

sudo service rabbitmq-server start (starts RabbitMQ server)
sudo rabbitmqctl list_queues (shows queue list)

sudo service apache2 start|graceful|graceful-stop|restart|stop or /etc/init.d/apache2 start|graceful|graceful-stop|restart|stop (graceful restarts apache2 gracefuly)
sudo a2ensite imesitea.com (enable virtual host site in apache. mod_rewrite module must be installed)
sudo a2dissite imesitea.com (disable virtual host site in apache) 
sudo a2enmod deflate (rewrite - omogućavanje apache2 modula deflate / rewrite )
sudo a2dismod

head -100 foo (output the first 100 lines of the file foo)
head -n-50 foo (output all lines from file but skip last 50 lines)
tail -f foo (output appended data as the file foo grows - very useful when monitoring log files)
tail -100 foo (output last 100 lines)
tail -n+50 foo (output all lines from file but skip first 50 lines)
cat foo (output the entire file in the standard output)

yes | nl | head -100 > foobar.txt (creates foobar.txt file that contains 100 lines, each line contains line numer and "yes" string)

tzselect (debian timezone select)

cat /proc/<pid>/limits (displays ulimits for the process with process id <pid>)

find /foo/bar/ -name "foobar*.pdf" -print0 | xargs -0 -I {} cp {} /tmp (find all pdf files in /foo/bar folder that are named foobar* and copy them to /tmp folder

apport /foo/bar/crash.report - opens apport crash log (check /var/crash or /var/log/apport.log usually contains additinal info about crash reports and coredumps)
gdb /usr/bin/php5 /path/to/coredump (this will open GNU debugger for the file and you can see backtrace with "bt" or "bt full")
apport-retrace -R -g _usr_bin_php5.1000.crash (will open gdb with the coredump extracted from the report)

which foo (locate a command foo that will be executed - useful for debugging PATH problems)
whereis foo (locate the binary, source, and manual page files for a command)
command -v foo (write a string to standard output that indicates the pathname or command that will be used by the shell - can be used in bash script instead of which to find what file will be executed in curr. environment)

whereis (locate binary, source and man pages for command)

cat foobar 2>&1 | tee bar.txt (redirect stderr to stdout, write it to the bar.txt file and display it to the screen)

!!!!!!!!!!!!!!!!!!!!!!!!!!!
MySQL
!!!!!!!!!!!!!!!!!!!!!!!!!!!
mysql -uroot -ppassword
mysqldump -uroot -ppassword --single-transaction --routines --triggers Foo > dumpfile.sql (safest way to dump database)


!!!!!!!!!!!!!!!!!!!!!!!!!!!
Mongo
!!!!!!!!!!!!!!!!!!!!!!!!!!!

use admin
db.runCommand({getCmdLineOpts:1}); ## displays options with which the mongod process was started (Command line parameters + parsed parameters from the config file)

mongodump -d dbNameFoo -o folderNameBar
mongorestore folderFoo

!!!!!!!!!!!!!!!!!!!!!!
GIT
!!!!!!!!!!!!!!!!!!!!!!

git init --bare (init empty git repository that will be a remote repo)
git remote add foo ssh://root@example.com/~/bar (add remote repository named foo on server example.com in folder ~/bar )
git push foo bar (push to remote repository foo branch bar)
git svn dcommit (commit to svn repository)
git checkout foobar (switch to branch foobar)
git clone -b foo file:///root/bar (clone branch foo from a local file)

git diff origin/master HEAD (diff the commited local changes with master branch on origin repo)
git rebase -i origin/master (interactive rebase to "squash" the commited changes on your local repo - WARNING - this changes history so use it only when you didn't push your changes to other repos)

!!!!!!!!!!!!!!!!!!!!!
HG
!!!!!!!!!!!!!!!!!!!!!

hg id (displays summary of the current state of the repository - useful for detecting revision of the working folder)
hg status --rev .:tip (dry run for update - compare the pulled changes with current status of the working directory)

!!!!!!!!!!!!!!!!!!!!!
SVN
!!!!!!!!!!!!!!!!!!!!!
svn update --set-depth exclude foobar (excludes folder from svn update - usefull when do not want to update large folders e.g. containing db data files)
svn update --set-depth infinity (restores the excluded folders so that they can be updated)

!!!!!!!!!!!!!!!!!!!!!
PUPPET
!!!!!!!!!!!!!!!!!!!!!

puppet describe -s (Prints help about Puppet resource types, providers, and metaparameters)
facter (collects and displays facts about system. Installed with puppet)


!!!!!!!!!!!!!!!!!!!!!
etckeeper
!!!!!!!!!!!!!!!!!!!!!

!!!!!!!!!!!!!!!!!!!!!
shell scripting
!!!!!!!!!!!!!!!!!!!!!

$1 (1st command line argument)
$n (n-th command line argument)
$0 (name by which the script has been invoked)
$# (number of arguments supplied, without $0)
$* (all arguments at once, but without $0)

local foo (defines local var in the function)

read (read one line from standard input - usefull when writing shell scripts and prompting user for info)

