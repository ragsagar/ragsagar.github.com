Shell Script to cipher a text file (caesar method)
##################################################
:date: 2009-05-27 22:20
:category: Gnu/Linux, Scripts, Shell Scripts

Ok here is a script to cipher text contents in a file. It will shift the
letters to the fifth letter to its right, ie if **a** is the letter, it
will change it to **f**. [sourcecode language='shell'] echo Enter the
filename read fn while read -n 1 letter do case $letter in '') echo ;; '
') printf ' ' ;; '.') printf '.' ;; \*) asci=$(printf %d \\'$letter)
((asci+=5)) fwd\_letter=$(printf "\\\\$(printf "%03o" $asci)") printf
"$fwd\_letter" ;; esac done < $fn [/sourcecode] You can decipher it by
just replacing the **+ in 18th line to-** Note : This is a assignment my
sis got from IGNOU. I hope this will help someone to do his/her
assignment :-)
