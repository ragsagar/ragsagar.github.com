Python code to find solution for jumbled word puzzle
####################################################
:date: 2011-07-24 15:14
:category: Python, Scripts

Here is a python script to find solution for a jumbled word. Give a
jumbled word as parameter, it will list the possible solutions.
[sourcecode language="python"] import sys dictfile =
"/usr/share/dict/cracklib-small" def get\_words(text): """ Return a list
of dict words """ return text.split() def
get\_possible\_words(words,jword): """ Return a list of possible
solutions """ possible\_words = [] jword\_length = len(jword) for word
in words: jumbled\_word = jword if len(word) == jword\_length: letters =
list(word) for letter in letters: if jumbled\_word.find(letter) != -1:
jumbled\_word = jumbled\_word.replace(letter,'',1) if not jumbled\_word:
possible\_words.append(word) return possible\_words if \_\_name\_\_ ==
'\_\_main\_\_': words = get\_words(file(dictfile).read()) if
len(sys.argv) != 2: print "python %s <jumbled word>" % sys.argv[0]
sys.exit() jumbled\_word = sys.argv[1] words =
get\_possible\_words(words,jumbled\_word) print "possible words :" print
'\\n'.join(words) [/sourcecode] Don't forget to change the 'dictfile' to
the wordslist file you have in your system. Here is the screenshot of
script output. `|image0|`_

.. _|image1|: http://ragsagar.files.wordpress.com/2011/07/unjumbled.png

.. |image0| image:: http://ragsagar.files.wordpress.com/2011/07/unjumbled.png
.. |image1| image:: http://ragsagar.files.wordpress.com/2011/07/unjumbled.png
