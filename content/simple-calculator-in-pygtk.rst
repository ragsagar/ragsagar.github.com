Simple Calculator using Pygtk
#############################
:date: 2008-12-07 20:27
:category: My_Works, Python, Scripts
:tags: calculator, gtk, gui, pygtk, Python, simple calculator

.. raw:: html

   <p>

I was working with pygtk for fewdays.It is pretty interesting.Suddenly
thoughts about making a calculator came into my mind.So i started
working on it.GUI designing was pretty easy when compared to the
calculation part. Finished the GUI part pretty fastly,but the
calculation part really made my head at sixes and sevens :-o.Anyway soon
i got a solution.In pygtk when a widget (eg button) is pressed it calls
a particular function.For that we connects the signal emitted from the
button with that function.So the calculation part should be in the
function that is called when the operators(+,-,/,\*) are pressed.The
function that executed when the numbers are pressed just sends that
number to the Text Entry widget (ie our calculator's screen).Hope you
got an idea abt the program! Any way it is well commented as far as i
can.So there wont be much problems to understand the code.As the code is
somewhat big iam not pasting it here..You can download it from `here`_
Run it using this command :

    python calculator.py

Here is its screenshot :- [caption id="attachment\_39" align="alignnone"
width="497"
caption="pygtk\_calculator"]\ |pygtk\_calculator|\ [/caption] Dont
forget to drop your comments , thanks :-)

.. raw:: html

   </p>

.. _here: http://ragsagar.freehostia.com/calculator.py

.. |pygtk\_calculator| image:: http://ragsagar.files.wordpress.com/2008/12/caclulator_pic.png
