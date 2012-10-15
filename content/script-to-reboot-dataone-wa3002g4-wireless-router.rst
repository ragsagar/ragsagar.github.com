Script to reboot dataone WA3002G4 wireless router
#################################################
:date: 2012-02-29 23:03
:category: Gnu/Linux, Scripts, Shell Scripts
:tags: expect, restart router, wa3002g4

With the WA3002G4 wireless router i got recently from my friend i made a
wifi hotspot in home. Haven't been downloading a lot since my `script to
reboot old teracom router`_ was not working with the new one.Thinking
that I should do something on the day which will come only in every four
years I modified the old script to work with the new wireless router and
I am sharing it here. [sourcecode language="bash"] #!/usr/bin/env expect
set username admin set pass admin set host 192.168.1.1 spawn telnet
${host} expect -re "Login:" send "${username}\\r" expect -re "Password:"
send "${pass}\\r" expect -re "Main Menu" send "13\\r" send "1\\r" expect
eof [/sourcecode]

.. _script to reboot old teracom router: http://ragsagar.wordpress.com/2011/08/13/script-to-reboot-teracom-router/
