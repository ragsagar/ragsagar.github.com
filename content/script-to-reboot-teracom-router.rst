Script to reboot teracom router
###############################
:date: 2011-08-13 05:53
:category: Scripts, Shell Scripts
:tags: expect, restart router

A slightly edited version of the script to restart router written by
`Madhusudan.C.S`_ to make it work with teracom router given by bsnl.
[sourcecode language="bash"] #!/usr/bin/env expect set username admin
set pass admin set host 192.168.1.1 spawn telnet ${host} expect -re
"Login:" send "${username}\\r" expect "Password:" send "${pass}\\r"
expect -re "successful" send "console enable\\r" send "restart\\r"
expect eof [/sourcecode]

.. _Madhusudan.C.S: http://www.madhusudancs.info/restart-router
