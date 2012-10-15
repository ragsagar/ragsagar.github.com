Python script that ranks Hollywood actors based on number of appearances in top 100 movies
##########################################################################################
:date: 2011-06-15 19:41
:category: Python, Scripts
:tags: actors ranking, codejam, imdb, imdbpy, Python

.. raw:: html

   <p>

Actually this is a sample question appeared in codejam contest conducted
by mobme wireless. Imdbpy python module is used to retrieve movie
informations from imdb. For those who don't know about this event :
http://codejam.mobme.in/ Sample Question :

    Write a program that ranks Hollywood actors based on the number of
    their appearances in a list of top 100 movies. There are a number of
    top movie lists on the Internet and it's up to you to choose one.
    We'd prefer you choose one that has an open API.

Solution in Python : [sourcecode language="python"] #!/usr/bin/env
python \_\_author\_\_ = "Rag Sagar.V" \_\_email\_\_ =
'@'.join(['ragsagar','.'.join([\_ for \_ in ['gmail','com']])]) from
twisted.internet import reactor, threads import re,imdb,itertools
actors\_rating = {} #actors\_rating['actor name'] = rank rank = 0 count
= 1 current\_rank = 0 concurrent = 5 finished = itertools.count(1)
reactor.suggestThreadPoolSize(concurrent) try: imdb\_access =
imdb.IMDb() except imdb.IMDbError, err: print err top\_100 =
imdb\_access.get\_top250\_movies()[:100] def populate\_actors(mid):
movie = imdb\_access.get\_movie(int(mid)) #print movie for i in (0,1):
actor\_name = movie['cast'][i]['name'] if
actors\_rating.has\_key(actor\_name): actors\_rating[actor\_name] =
actors\_rating[actor\_name] + 1 else: actors\_rating[actor\_name] = 1 if
finished.next()==added: reactor.stop() added = 0 for movie in top\_100:
added += 1 req = threads.deferToThread(populate\_actors, movie.getID())
try: reactor.run() except KeyboardInterrupt: reactor.stop() for actor in
sorted(actors\_rating, key=actors\_rating.get, reverse=True):
previous\_rank = current\_rank current\_rank = actors\_rating[actor] if
previous\_rank != current\_rank : rank += count count = 1 else: count +=
1 print rank,actor [/sourcecode] Dependency : imdbpy

.. raw:: html

   </p>

