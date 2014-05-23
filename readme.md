#LoadWatch 

### Email notification + diagnostics emailed when a preset server load is triggered.  

* loadwatch_cpanel.sh - for WHM/cPanel servers running on Centos
* loadwatch_ubuntu.sh - ubuntu servers running nginx


### Install

**Using git + our init script:**

This is the fastest way to get up and running. Let us handle the installation for you!

```
cd /root; git clone https://github.com/getresults/loadwatch.git;
cd loadwatch
sh bin/loadwatch_cpanel.sh --init
```

**Using git:**

```
cd /root
git clone https://github.com/getresults/loadwatch.git
cd loadwatch/bin
cp loadwatch_cpanel.sh loadwatch.sh
chmod u+x loadwatch.sh
chmod u+x thirdparty/mysqltuner.pl
```

**To install loadwatch.sh manually:** 

```
mkdir /root/loadwatch
mkdir /root/loadwatch/bin/
touch /root/loadwatch/bin/loadwatch.sh
chmod u+x /root/loadwatch/bin/loadwatch.sh
vim /root/loadwatch/bin/loadwatch.sh
```
Copy and paste the contents of the correct loadwatch.sh into vim and save. 

Copy loadwatch_ubuntu.sh to loadwatch.sh if on an Ubuntu based server

### Configure

Edit loadwatch.sh and set the LOAD level and EMAIL address you want to use for notifications.

For a single CPU server using '4' for the load level is fairly typical. 


### Set up Cron

Next, edit your crontab and insert the entry below which will run loadwatch.sh every 20 minutes to check server load and generate a report of the load is over the set threshold.

```
crontab -e  

*/3 * * * * /root/loadwatch/bin/loadwatch.sh > /dev/null 2>&1
```

Make sure the loadwatch script is set to 700 permissions. 

### Warning

Log files are not deleted or trimmed currently and will continue growing over time.  


### Acknowledgements

* An awesome LiquidWeb.com staff member who gave me a copy of the base script.


### Disclaimer

* Use at your own risk - no warranty or support is provided. 

### Todo

* Improve Ubuntu version to match 'sar' type reporting if possible.
* Add nginx / typical ubuntu email agent debug info to loadwatch_ubuntu.sh
* Look for ways to expand the script to provide more relevant info
	* Here: http://forums.cpanel.net/f34/troubleshooting-high-server-loads-linux-servers-319352.html 
	* Notes stored under 'Server' in Evernote

