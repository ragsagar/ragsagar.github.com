Script for appending Title of Song Playing in Rhythmbox as Status Message in Pidgin
###################################################################################
:date: 2009-03-10 22:48
:category: Gnu/Linux, Howtos, Python, Scripts
:tags: Current Track, dbus, Now Playing, Pidgin, Python, rhythmbox, status updating

.. raw:: html

   <p>

Yesterday i installed debian lenny ( thanks to `ashik salahudeen`_ who
sent me those DVDs for free :-) ). I was not ready to waste another
holiday.So started thinking of doing something and got landed in my
usual plugin stuff.This time not audacious,its Rhythmbox.So downloaded
my pidgin-audacious now playing code and rewritten it to access
rhythmbox methods.This time there is a lot of changes in the code.This
code is not going to use 'watch' command to execute it after a fixed
period and another interesting feature is a format specifier kinda
thing. ie Just write what you want in the status message and place a
format specifier where you want to see the song title , album title and
artist. Format Specifiers are

    **%rbs --------------> for displaying song title %rbt
    --------------> for displaying album title %rba --------------> for
    displaying artist name**

Script will append a seperate string containg songtitle and albumtitle
if no format specifier is there in the status message at the time of
running the script. An example for appending status message using format
specifier kinda thing:

    **%rbs in %rbt by %rba**

[caption id="attachment\_64" align="alignnone" width="249"
caption="pidgin after appending format specifier kinda thing in status
message"]\ |pidgin-after-appending-formatspecifier kinda thing in status
message|\ [/caption] Now download the script and run it using these
commands

    **$wget http://ragsagar.freehostia.com/pidgin-rb.py $python
    pidgin-rb.py**

[caption id="attachment\_73" align="alignnone" width="500"
caption="Downloading and running the script"]\ |Downloading and running
the script|\ [/caption] [caption id="attachment\_65" align="alignnone"
width="249" caption="pidgin after running the script"]\ |pidgin after
running the script|\ [/caption] **PS : Run the script only after
appending the format specifier kinda thing. You can run the script
without appending anything, In this case the script will append status
message like " listening to [songname] in [albumname] "**

    **`Download Script`_**

.. raw:: html

   </p>

.. _ashik salahudeen: http://aashiks.in
.. _Download Script: http://ragsagar.freehostia.com/pidgin-rb.py

.. |pidgin-after-appending-formatspecifier kinda thing in status
message| image:: http://ragsagar.files.wordpress.com/2009/03/pidb4run3.png
.. |Downloading and running the
script| image:: http://ragsagar.files.wordpress.com/2009/03/terminal.png
.. |pidgin after running the
script| image:: http://ragsagar.files.wordpress.com/2009/03/pidafterrun.png
