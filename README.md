# updateOmbi

### Notes:
The assumptions for this script are that you are using Linux for your Ombi and the service is controlled with systemd.  
 
There are several variables in use you can change to suit your environment:
> * SERVICE_NAME=ombi				# Change this if your systemd service is not named 'ombi'
> * KEEP_BACKUP=no				# Change this to 'yes' if you'd like to keep the previous installation as backup
> * SLACK_WEBHOOK=				# If you'd like to use Slack for updates then input your Webhook you can get from Slack integrations.  If not using Slack, then no need to change this.
> * SLACK_MESSAGE="Upgrading Ombi to v$VERSION" # Adjust if you'd like a different message to the Slack alert
> * SLACK_CHANNEL=alerts			# Adjust to the channel you'd use in Slack
> * SLACK_USER=ombi				# Change to the user you'd like the message to come through as.  It should be dynamic though so no need to change.

This works as a script you can put in (`cp /link/to/script/updateOmbi.sh /etc/cron.daily`) or symlink to (`ln -s /link/to/script/updateOmbi.sh /etc/cron.daily`) in /etc/cron.daily or hourly  
That will run it as root  
If you'd like it to not run it as root, then you should use `visudo` to add `ombi    ALL=NOPASSWD: /bin/systemctl stop ombi.service, /bin/systemctl start ombi.service` to the sudoers file  
Then you could run it under `/var/spool/cron/ombi` as an entry such as `0 0 0 ? * * * /link/to/script/updateOmbi.sh` and that would run it daily at midnight  
