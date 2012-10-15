Now Playing script for pidgin and audacious
###########################################
:date: 2008-11-21 22:39
:category: Gnu/Linux, My_Works, Python, Scripts, Shell Scripts
:tags: Audacious, dbus, Now Playing, Pidgin, Py-dbus, Python

.. raw:: html

   <p>

Few days ago i wrote a script to update the status message in pidgin
with the title of the song playing in audacious music player.It is
written in python.it makes use of the dbus for the inter application
communication.when you invoke that script it just appends the title of
the song currently playing in audacious as the status message in pidgin
.i used the shell command $watch to invoke it in every 30 seconds so
that the status message gets updated with the songtitle within 30
seconds after the song change.You can reduce the number of seconds so
that the status message gets updated frequently reducing the time delay
between the song change and updation of status message.What the script
does is, it retrieves the song title from the audacious music player
using dbus.Then this songtitle is assigned as the status message in
pidgin by communicating through dbus.This script needs dbus and
py-dbus.So make sure that you have both packages installed in your
system. Here is the script :

    def set\_message(message): # Get current status type
    (Available/Away/etc.) current =
    purple.PurpleSavedstatusGetType(purple.PurpleSavedstatusGetCurrent())
    # Create new transient status and activate it status =
    purple.PurpleSavedstatusNew("", current) msg="Now Playing: "
    emsg=msg+message purple.PurpleSavedstatusSetMessage(status, emsg)
    purple.PurpleSavedstatusActivate(status) import dbus
    session\_bus=dbus.SessionBus() proxy =
    session\_bus.get\_object("im.pidgin.purple.PurpleService",
    "/im/pidgin/purple/PurpleObject") purple = dbus.Interface(proxy,
    "im.pidgin.purple.PurpleInterface") proxy1 =
    session\_bus.get\_object('org.mpris.audacious','/TrackList') purple1
    = dbus.Interface(proxy1,'org.freedesktop.MediaPlayer') ct =
    purple1.GetCurrentTrack() proxy2 =
    session\_bus.get\_object('org.mpris.audacious','/org/atheme/audacious')
    purple2 = dbus.Interface(proxy2,'org.atheme.audacious') currentsong
    = purple2.SongTitle(ct) print currentsong set\_message(currentsong)

Running this script will update the status message just once , so u have
to shell command $watch as i said earlier.if you dont want to do this
things manually, dont worry! i got package for this, grab it from here
http://ragsagar.freehostia.com/pidgin-audacious\_plugin.tar.gz , untar
it and run the installer..

    $wget http://ragsagar.freehostia.com/pidgin-audacious\_plugin.tar.gz
    $tar -xvf pidgin-audacious\_plugin.tar.gz $cd pidgin-audacious\\
    plugin/ $sudo chmod a+x installer $./installer

Now run the script using this command :

    $pidgin-plugin

PS: Make sure that you have both audacious and pidgin already running

.. raw:: html

   </p>

