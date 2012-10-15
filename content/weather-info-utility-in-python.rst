Weather Info Utility in Python
##############################
:date: 2009-07-21 21:37
:category: My_Works, Python, Scripts
:tags: google api, Python, urllib2, weather, xml

Here is a script to provide weather information of a city with the help of google api.
''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''

[sourcecode language="python"] #!/usr/bin/python #Rag Sagar #Free to
copy, modify and redistribute import sys from urllib2 import urlopen,
URLError from xml.sax import make\_parser from xml.sax.handler import
ContentHandler class WeatherFinder(ContentHandler): """the handler
class""" def \_\_init\_\_(self): self.weather\_list = [] self.go\_on =
False def startElement(self, tag, attrs): "handles the opening tags" if
tag == 'current\_conditions': self.go\_on = True if self.go\_on : # so
that only values inside current\_conditions tag is appended if tag ==
'condition' : self.weather\_list.append('Condition:
'+attrs.get('data',"")) elif tag == 'humidity' :
self.weather\_list.append(attrs.get('data',"")) elif tag == 'temp\_c' :
self.weather\_list.append('Temperature:'+attrs.get('data',"")+'C') elif
tag == 'wind\_condition' :
self.weather\_list.append(attrs.get('data',"")) return def
endElement(self, tag): "handles closing tags" if tag ==
'current\_conditions': self.go\_on = False if len(sys.argv) is not 2 :
print "Syntax : ",sys.argv[0]," \\n" sys.exit(1) else : city =
sys.argv[1] url = 'http://www.google.com/ig/api?weather='+city parser =
make\_parser() obj = WeatherFinder() parser.setContentHandler(obj) try :
parser.parse(urlopen(url)) except URLError: print "\\n\\33[33m Unable to
fetch data..\\33[0m\\n" sys.exit(1) if obj.weather\_list == [] : print
"\\n\\33[33m Invalid city name, Try another.. \\33[0m\\n " else : print
"\\33[33mWeather Conditions of",city,"\\33[36m" for i in
obj.weather\_list: print i print "\\33[0m" [/sourcecode] Checkout its
screenshot [caption id="attachment\_120" align="alignnone" width="499"
caption="Weather utility "]|Weather utility|\ [/caption] Thanks to
`rohit`_

.. raw:: html

   </p>

.. _rohit: http://linrdx.blogspot.com

.. |Weather
utility| image:: http://ragsagar.files.wordpress.com/2009/07/screenshot_weather.png
