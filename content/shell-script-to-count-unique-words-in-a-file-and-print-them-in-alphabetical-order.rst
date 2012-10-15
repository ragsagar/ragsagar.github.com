Shell script to count unique words in a file and print them in alphabetical order
#################################################################################
:date: 2009-05-30 19:00
:category: Gnu/Linux, Scripts, Shell Scripts
:tags: assignment, bash, IGNOU, shell script, unique words, unique words count

Iam back with another shell script written for my sis as part of her
assignment. This time what i wanted to do is to count the unique words
in a file and to print it in alphabetical order. For that i iterated
through the words in the given file using for loop, filtered out the
unique words using sort -u and counted it using wc -l. [sourcecode
language='shell'] #!/usr/bin/bash echo Enter the filename read fn for
WORD in $(cat $fn) do echo "$WORD" done \| sort -u \| wc -l for WORD in
$(cat $fn) do echo "$WORD " done \| sort -u [/sourcecode] Hope this will
help someone to do his/her assignment :-D
