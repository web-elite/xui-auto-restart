[🇮🇷](https://github.com/web-elite/xui-auto-restart/blob/main/README-fa.md) | [🇺🇸]([/guides/content/editing-an-existing-page](https://github.com/web-elite/xui-auto-restart/blob/main/README.md))
# X-ui Auto Restart
Automatically restart xui using this tutorial

#### Tutorial

1. Create a shell script
First create a shell script that will execute the x-ui restart command.

```
sudo nano /usr/local/bin/x-ui-restart.sh
```
And put the following content in it:

```
#!/bin/bash
x-ui restart
```
Then save the file and exit.

2. Grant the script execution permission
Run the following command to make the script executable:

```
sudo chmod +x /usr/local/bin/x-ui-restart.sh
```
3. Create a timer with Systemd
Create a Systemd service file:

```
sudo nano /etc/systemd/system/x-ui-restart.service
```
And put the following content in it:

```
[Unit]
Description=Restart x-ui service

[Service]
ExecStart=/usr/local/bin/x-ui-restart.sh
```
Save the file and exit.

4. Create a timer to run every hour
Create the timer file:

```
sudo nano /etc/systemd/system/x-ui-restart.timer
```
The following timer file content will run automatically every 1 hour.
Enter the following content:

```
[Unit]
Description=Run x-ui restart every hour

[Timer]
OnBootSec=1min
OnUnitActiveSec=1h
Unit=x-ui-restart.service

[Install]
WantedBy=timers.target
```
⚠️ Note that the value 1h means one hour, you can change the value as you wish.

5. Enable and run the timer
Run the following commands:
```
sudo systemctl daemon-reload
```
```
sudo systemctl enable x-ui-restart.timer
```
```
sudo systemctl start x-ui-restart.timer
```
6. Check the status of the timer
To make sure the timer is working properly, run the following command:

```
sudo systemctl list-timers --all
```
You should see the x-ui-restart.timer timer showing the next time it will run.
