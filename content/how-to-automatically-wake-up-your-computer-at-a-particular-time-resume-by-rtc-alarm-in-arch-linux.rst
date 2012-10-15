How to automatically wake up your computer at a particular time ( Resume by RTC alarm in Arch Linux )
#####################################################################################################
:date: 2011-08-15 14:04
:category: Howtos
:tags: acpi, alarm, arch, automatic booting, automatic wakeup, how-to, linux, resume by rtc, RTC, wakeup

My ISP provides unlimited download from 2am to 8am. So i was not able to
sleep after 2 from the time i switched to the new broadband plan.
Keeping the system on and setting a cronjob to start downloading after 2
was an option. But i was more concerned about the increasing electricity
charge, than my sleep. Besides it is my social responsibility to save
energy as a gonna-be software engineer :p. After a bit of googling and
hacking i was able to wake up my system at a particular time. Here i am
going to explain how i made my arch linux system to boot automatically
at 2 am. The configuration is done in Arch Linux. For automatic wakeup
it needs a BIOS which supports RTC alarm. Most of them manufactured
after 2000 supports this feature.

1) Check if your BIOS supports automatic wakeup
-----------------------------------------------

Execute the command below as root. [sourcecode language="text"]# grep
rtc /var/log/messages.log rtc\_cmos 00:03: RTC can wake from S4 rtc0:
alarms up to one month [/sourcecode] If you can find something like this
in the output.It says that the system can wakeup and a wakeup time can
be setup.

2) Enable automatic wakeup in BIOS
----------------------------------

Go to your BIOS setup, Under Power Management search for something like
"Wake by RTC Alarm" or "Resume by RTC alarm" or "RTC resume".Then enable
it.

3) Set the hardware clock time standard as UTC
----------------------------------------------

Edit the /etc/rc.conf file as root and set the HARDWARECLOCK variable to
UTC [sourcecode language="text"][ragsagar@h4ckb0x ~]$ grep
^HARDWARECLOCK /etc/rc.conf HARDWARECLOCK="UTC"[/sourcecode] Make sure
that your timezone is set correctly in /etc/rc.conf More help :
https://wiki.archlinux.org/index.php/Time

4) Set the alarm time
---------------------

Execute the following commands as root [sourcecode language="text"]#
echo 0 > /sys/class/rtc/rtc0/wakealarm # echo \`date '+%s' -d '+ 5
minutes'\` > /sys/class/rtc/rtc0/wakealarm [/sourcecode] This will set
the the alarm time as 5 minutes into the future. `|image0|`_ Now run
[sourcecode language="text"]$ cat
/sys/class/rtc/rtc0/wakealarm[/sourcecode] If the output of above
command is something like "1313383930", the alarm is set. It is epoch
time. If it doesn't yield any result make sure that the HARDWARECLOCK
variable is set to UTC and reboot and try again to set the alarm time.
Now run [sourcecode language="text"]$ cat /proc/driver/rtc [/sourcecode]
`|image1|`_ Go through rtc\_time, alrm\_time and alrm\_date and check if
they are correct(will be in UTC).Turn off the system and leave the power
on. Check if the system is booting automatically after five mintues.

5) Setting the alarm to a particular time and date.
---------------------------------------------------

To set the alarm to woke up the system at 16th Aug 2:05am, Run the
following as root [sourcecode language="text"]# echo 0 >
/sys/class/rtc/rtc0/wakealarm # date --date "Aug 16 , 2011 02:05:00" +%s
> /sys/class/rtc/rtc0/wakealarm[/sourcecode] You can convert the epoch
time to readable format and check the alarm time is correct. [sourcecode
language="text"][root@h4ckb0x ragsagar]# cat
/sys/class/rtc/rtc0/wakealarm 1313440500 [root@h4ckb0x ragsagar]# date
-d @1313440500 +%F" "%T 2011-08-16 02:05:00 [/sourcecode] `|image2|`_
**Note :** The mythtv wiki about acpi wakeup says that setting the
hardware clock after setting alarm will disable the alarm while most of
the linux distribution sets hardware clock during shutdown. They suggest
to disable hardware clock adjusting during shutdown. To do that in
Archlinux set the HARDWARECLOCK="" in /etc/rc.conf . But in my arch
system the alarm was not working when i set HARDWARECLOCK="" whereas it
worked when i gave HARDWARECLOCK="UTC". So if the wake up alarm is not
working do try after changing the value of this variable. To start
downloading when the system boots up, i added a cronjob to `restart the
router`_ at 2:15 and 7:45 (to account the download in happy hours). Also
added "transmission-gtk" to the gnome-session-properties. So that
transmission will be launched on startup and downloading will be
started. **Reference :** http://www.mythtv.org/wiki/ACPI\_Wakeup
https://wiki.archlinux.org/index.php/Time

.. raw:: html

   </p>

.. _|image3|: http://ragsagar.files.wordpress.com/2011/08/set_alarm_5.png
.. _|image4|: http://ragsagar.files.wordpress.com/2011/08/proc_driver_rtc.png
.. _|image5|: http://ragsagar.files.wordpress.com/2011/08/particular_tme.png
.. _restart the router: http://ragsagar.wordpress.com/2011/08/13/script-to-reboot-teracom-router/

.. |image0| image:: http://ragsagar.files.wordpress.com/2011/08/set_alarm_5.png
.. |image1| image:: http://ragsagar.files.wordpress.com/2011/08/prod_driver_rtc.png
.. |image2| image:: http://ragsagar.files.wordpress.com/2011/08/particular_tme.png
.. |image3| image:: http://ragsagar.files.wordpress.com/2011/08/set_alarm_5.png
.. |image4| image:: http://ragsagar.files.wordpress.com/2011/08/prod_driver_rtc.png
.. |image5| image:: http://ragsagar.files.wordpress.com/2011/08/particular_tme.png
