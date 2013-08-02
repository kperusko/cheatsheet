pkill -f procnamex (kills all processes with name procnamex)
ps -aux | grep procnamex (show all processes with name procnamex)
ps -p $$ (displays the current shell you're using)
pstree -a (display a tree of processes with command line arguments)
kill -9 12030 (kills process with PID 12030. -9 sends KILL signal to process so use it only when absolutely necessary)

man -k foo (search foo in man pages descriptions)
man -wK foo (search foo in man pages bodies)

echo $? (reads the exit status of the last command executed. After a function returns, $? gives the exit status of the last command executed in the function)
echo $$ (displays the current process PID)
echo $! (displays the PID of the last backgrounded process)
sudo update-rc.d foobar defaults (installs the init script foobar for all run levels - foobar script must be in the /etc/init.d/. This will enable to call service foobar start)

top (show linux tasks / processes)
htop (proces monitor)
atop (resource monitor)

w (who is logged and what they are doing)
last (show listing of last logged in users)

free -m (display amount of free and used memory in the system -m in MB)
dmidecode (displays DMI (SMBIOS) - all system information)
iostat (I/O statistics for devices and partitions)
iotop (top-like I/O monitor)
netstat (network statistics tool usefull in analyzing network connections, routing tables, network interfaces)
ifstat (ethernet  traffic monitor)
apachetop -f /var/log/apache2/access.log (displays real-time web server statistics)
dstat (generating system resources - usefull monitor tool)

history (show history of all commands in shell) - bash history is written in the file ~/.bash_history
history -c (deletes shell history from RAM)
export HISTTIMEFORMAT="[%F] [%T] " (set the HISTTIMEFORMAT variable so that the history contains date and time for each command - only for current session - add to ~/.bash_profile to make it permanent)

sysctl -a (display all kernel parameters at runtime)
lsb_release -a (displays version of a ubuntu OS)
uname -a (more general system information)
cat /proc/cpuinfo (display info about cpu)

tar cvf foo.tar bar/ (creates tar archive with name foo.tar from the folder bar)
tar xvf foo.tar (extracts tar in current directory)

sed -i "s/foo/bar" bazfile (inplace search and replace in files - replaces foo with bar in file bazfile)

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
	
ssh -f -N foobar (open local port fowarding: -f execute in background, -N don't execute remote command)

foobar can be anyname you like
LocalForward/IdentityFile is optional
-----------------

sftp root@hostname.example.com  (SFTP connection to remote server)
get Foo.txt (with connected with sftp gets the file Foo.txt from remote server)

sudo su (login as super user)

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

touch foo.bar (create file with name foo.bar)
echo "foobar" > foo.bar (creates file foo.bar if doesn't exists or overwrites existing file and writes foobar inside)
echo "foobar" >> foo.bar (creates file foo.bar if doesnt exists and writes foobar inside, appends to the file if file already exits)

vim imefilea.txt ili vi imefilea.txt (opens text editor VIM)
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
apt-get update (updates versions of the apps)
apt-get purge packageNameFoo (deletes packageNameFoo program)

apt-cache show packageNameFoo (displays detailed info about current and installed package)
apt-cache policy packageNameFoo (displays only verision info about current and installed package)

sudo service rabbitmq-server start (starts RabbitMQ server)
sudo rabbitmqctl list_queues (shows queue list)

sudo service apache2 start|graceful|graceful-stop|restart|stop or /etc/init.d/apache2 start|graceful|graceful-stop|restart|stop (graceful restarts apache2 gracefuly)
sudo a2ensite imesitea.com (enable virtual host site in apache. mod_rewrite module must be installed)
sudo a2dissite imesitea.com (disable virtual host site in apache) 
sudo a2enmod deflate (rewrite - omogućavanje apache2 modula deflate / rewrite )
sudo a2dismod

head foo (output the first part of the file foo)
tail foo (output the last part of the file foo)
cat foo (output the entire file in the standard output)

tzselect (debian timezone select)

cat /proc/<pid>/limits (displays ulimits for the process with process id <pid>)

find /foo/bar/ -name "foobar*.pdf" -print0 | xargs -0 -I {} cp {} /tmp (find all pdf files in /foo/bar folder that are named foobar* and copy them to /tmp folder

apport /foo/bar/crash.report - opens apport crash log (check /var/crash or /var/log/apport.log usually contains additinal info about crash reports and coredumps)
gdb /usr/bin/php5 /path/to/coredump (this will open GNU debugger for the file and you can see backtrace with "bt" or "bt full")
apport-retrace -R -g _usr_bin_php5.1000.crash (will open gdb with the coredump extracted from the report)


which foo (locate a command foo that will be executed - useful for debugging PATH problems)
command -v foo (write a string to standard output that indicates the pathname or command that will be used by the shell - can be used in bash script instead of which to find what file will be executed in curr. environment)

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

!!!!!!!!!!!!!!!!!!!!!
HG
!!!!!!!!!!!!!!!!!!!!!

hg id (displays summary of the current state of the repository - useful for detecting revision of the working folder)
hg status --rev .:tip (dry run for update - compare the pulled changes with current status of the working directory)

!!!!!!!!!!!!!!!!!!!!!
SVN
!!!!!!!!!!!!!!!!!!!!!
svn update --set-depth exclude foobar (excludes folder from svn update - usefull when don't want to update large folders e.g. containing db data files)
svn update --set-depth infinity (restores the excluded folders so that they can be updated)

!!!!!!!!!!!!!!!!!!!!!
PUPPET
!!!!!!!!!!!!!!!!!!!!!

puppet describe -s (Prints help about Puppet resource types, providers, and metaparameters)
facter (collects and displays facts about system. Installed with puppet)


!!!!!!!!!!!!!!!!!!!!!
etckeeper