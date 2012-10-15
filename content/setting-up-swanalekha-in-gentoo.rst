Setting up swanalekha in Gentoo!
################################
:date: 2008-11-20 14:27
:category: Gnu/Linux, Howtos
:tags: Gentoo, Malyalam, Scim, Swanalekha

.. raw:: html

   <p>

Swanalekha is a scim malayalam phonetic input method.We can type
malayalam easily using swanalekha as it uses transliteration based input
method! Iam going to explain(not really :p) how i installed swanalekha
in my gentoo installation! As it is scim based, swanalekha definitely
needs scim,so we have to install it frist.To install it you can use
emerge command.it downloads and compiles its source and solves
dependecies by itself,so need to worry about dependecy! If you want to
know the size and list of dependencies of scim that emerge downloads,
use this command..

    #emerge -pv scim

Install it using this command :

    #emerge scim

Swanalekha needs another two packages named scim-tables and
scim-m17n,they wont get installed with scim, so install them manually
using this command..

    #emerge scim-tables scim-m17n

Now get the source tarball from
http://savannah.inetbridge.net/smc/Swanalekha/swanalekha\_0.3.1\_2.tar.gz
untar it and cd into it..

    $tar -xvf swanalekha\_0.3.1\_2.tar.gz

    $cd swanalekha\_0.3.1\_2

now run make as root

    #make

now configure scim and run

    $scim-setup

[caption id="attachment\_9" align="alignnone" width="331"
caption="scim-setup window"]\ `|scim-setup window|`_\ [/caption] In the
Global Setup tab under IMengine enable Malayalam.Restart scim for the
changes to take effect.Now open your favourite text editor.Right click
and select Scim Input Method from Input Methods.Then left click in the
scim tray icon,select Malalyalam-Swanalekha from it and start typing
malayalam! `|malayalam typed using swanalekha in leafpad texteditor|`_
PS: Hope you have malayalam fonts installed,otherwise get some fonts
from `here`_ and copy it to ~/.fonts or /usr/share/fonts and restart x

.. raw:: html

   </p>

.. _|image2|: http://ragsagar.files.wordpress.com/2008/11/scim-setup.png
.. _|image3|: http://ragsagar.files.wordpress.com/2008/11/swana_leafpad.png
.. _here: http://download.savannah.gnu.org/releases/smc/fonts/malayalam-fonts-04/

.. |scim-setup
window| image:: http://ragsagar.files.wordpress.com/2008/11/scim-setup.png
.. |malayalam typed using swanalekha in leafpad
texteditor| image:: http://ragsagar.files.wordpress.com/2008/11/swana_leafpad.png
.. |image2| image:: http://ragsagar.files.wordpress.com/2008/11/scim-setup.png
.. |image3| image:: http://ragsagar.files.wordpress.com/2008/11/swana_leafpad.png
