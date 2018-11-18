Setup as a service on Linux
===========================

In GNU/Linux, the recommended way of setting up the bot as a service is using [systemd](https://en.wikipedia.org/wiki/Systemd). It is installed by default on all distros I've used, from both the Debian and Red Hat branches of Linux

Setting TediCross up as a service means it will automatically start during boot, and will also try to restart itself if it crashes.

Only the first part (Setting up the service) is strictly necessary, but the rest give you nice log files


Setting up the service
----------------------

The setup is quite simple. Make the file `/etc/systemd/system/heimdall.service` and populate it with the following:

```
[Service]
ExecStart=/usr/bin/npm start
WorkingDirectory=/home/user/Heimdall
Restart=always
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=tedicross
User=tedicross
Group=tedicross
Environment=TELEGRAM_BOT_TOKEN=secret
Environment=DISCORD_BOT_TOKEN=secret

[Install]
WantedBy=multi-user.target
```

Adjust the file to suit your needs. I have Heimdall running as a dedicated user `heimdall`, but you can use any user. `root` will work, but is NOT recommended!

Also point `WorkingDirectory` to wherever your Heimdall files are

You can, if you want to, supply the bot tokens through the service file. Put them at their respective lines in the file. This requires that `token` in TediCross' `settings.json` is set to `"env"`. If you prefer to give the tokens through `settings.json`, just remove the two lines starting with `Environment`

When you are happy with the file, run the command `systemctl enable heimdall`. This activates the service. You can then control the service and check its status with the commands `systemctl start|stop|restart|status heimdall` (pick one of the middle words).

Note that after editing the service file, you need to run the command `systemctl daemon-reload` followed by `systemctl restart heimdall` to apply them

