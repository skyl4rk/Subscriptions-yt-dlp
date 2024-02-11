# Subscriptions-yt-dlp
Bash script to regularly download new video from a list of channels 

#!/bin/bash
#Subscriptions.sh

#Check for new videos every hour from channel list and download them.

date > /home/pi/cron/subscriptions_output.txt

timeout 59m /usr/local/bin/yt-dlp -S "res:1080" -P /media/pi/E24F-8639/Subscriptions/ --restrict-filenames -o '%(upload_date)s-%(channel)s-%(title)s-%(id)s.%(ext)s' --dateafter today-1days --playlist-end 3 -a /home/pi/Desktop/Subscriptions --throttled-rate 2K -R 100 --download-archive /home/pi/cron/subscription_archive 1>>/home/pi/cron/subscriptions_output.txt

date >> /home/pi/cron/subscriptions_output.txt

#1. Save this file as /home/pi/cron/Subscriptions.sh, or modify the path as desired. 

#2. Make the file executable.

#3. Change -P /media/pi/E24F-8639/Subscriptions/ to reflect the desired path to storage.

#4. Using $which yt-dlp, change path to yt-dlp executable: /usr/local/bin/yt-dlp.

#5. Create a textfile: /home/pi/Desktop/Subscriptions. On each line, write a url using the format: YT Video Channel:Videos:Play All, "Copy Link". Write the name of the channel using the format: #Channel Name. Modify the path /home/pi/Desktop/Subscriptions to reflect your desktop path.

#6. Modify the path /home/pi/cron/subscription_archive and /home/pi/cron/subscriptions_output.txt to your desired location for log and archive text files, which will be created by the script.  

#7. Set up a scheduled action to run this script using crontab, modify the path and filename as in step 1.

#8. $crontab -e
## 0 * * * * bash /home/pi/cron/Subscriptions.sh

