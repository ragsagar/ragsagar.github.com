Python script to find Imdb rating
#################################
:date: 2010-11-20 10:31
:category: Uncategorized
:tags: BeautifulSoup, command line, imdb, mechanize, movie, Python, rating, script

Here is a script i wrote last night.It finds imdb rating of a movie.
[sourcecode language="python"] #ragsagar[at]gmail.com from mechanize
import Browser from BeautifulSoup import BeautifulSoup import sys,re if
len(sys.argv) != 2: print "\\nSyntax: python %s 'Movie title'" %
(sys.argv[0]) exit() else : movie = '+'.join(sys.argv[1].split()) br =
Browser() br.open("http://www.imdb.com/find?s=tt&q="+movie) link =
br.find\_link(url\_regex = re.compile(r"/title/tt\*")) res =
br.follow\_link(link) soup = BeautifulSoup(res.read()) try : title =
soup.find('h1').contents[0].strip() rating =
soup.find('span',attrs='rating-rating').contents[0] print "Movie :
",title print "Rating: ",rating,"/ 10.0" except : print "Not Found!"
[/sourcecode] Here is the screenshot of output. [caption
id="attachment\_171" align="alignnone" width="300" caption="Output of
the script"]\ `|image0|`_\ [/caption]

.. _|image1|: http://ragsagar.files.wordpress.com/2010/11/imdbscreenshot.png

.. |image0| image:: http://ragsagar.files.wordpress.com/2010/11/imdbscreenshot.png?w=300
.. |image1| image:: http://ragsagar.files.wordpress.com/2010/11/imdbscreenshot.png?w=300
