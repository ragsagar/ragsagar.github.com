Display wishes depending on time when you open the console
##########################################################
:date: 2011-06-07 23:12
:category: Python, Scripts
:tags: bashrc, Python, time

.. raw:: html

   <p>

Here is a python script to wish you Good Morning or Good Evening
according to the time of the day. [sourcecode language="python"]
#!/usr/bin/python import time current\_hour =
time.strptime(time.ctime(time.time())).tm\_hour if current\_hour < 12 :
print "Good Morning!" elif current\_hour == 12 : print "Good Noon!" elif
current\_hour > 12 and current\_hour < 18 : print "Good AfterNoon!" elif
current\_hour >= 18 : print "Good Evening!" [/sourcecode] Now if you
want to display it when you open the console add the following line to
your ~/.bashrc file.

    python /path/to/the/script.py

Happy Hacking! :)

.. raw:: html

   </p>

