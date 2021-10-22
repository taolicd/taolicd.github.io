---
layout: post
title:  "A peek into HTML, XML, XHTML, JSON, and Markdown"
date:   2019-04-23
use_math: false
comments: true
---

## HTML
HTML is a standard markup language designed for creating web pages. The initial HTML 1 was released in 1991 and the most current version is HTML 5. 

HTML has a pre-defined set of tags, which means you cannot create your own tags.

You can embed script languages such as JavaScript (including JSON, more on JSON later) in HTML to add functionality to a web page.

## XML

XML is an extendable markup language designed with data exchange in mind. The initial release was in 1996. The latest version is still XML version 1.0.

 XML tags are user-defined and each XML file needs its own DTD or schema to validate against. DTD or schema defines the data structure that is permitted for a particular XML file. (The difference between DTD and schema is out of the scope of this discussion.)

XML is not a replacement of HTML nor a rival. The rivals of XML are relational databases and JSON. 


## XHTML
 XHTML is an XML-ized HTML that complies with both HTML and XML standards. XHTML was initially released in 2000. The latest version is XHTML 5, which adopts HTML5 standards.

XHTML is considered better than HTML because it is in essence an XML format, which means it is more extensible and interoperable with other data formats. 


XHTML can be a candidate to replace HTML. However as of today lots of people still believe HTML5 is for the masses and XHTML5 is not.  

There are tools available to convert HTML to XHTML. An example is [html2xhtml](http://www.it.uc3m.es/jaf/html2xhtml/).


## JSON

JSON is a lightweight data interchange format for the web. JSON is part of Javascript. Because Javascript is a scripting language that can be embedded within HTML, you can directly use JSON in an HTML page. JSON was invented in 2002. 

JSON denotes data objects in key-value pairs and is gaining wide adoption because it is much simpler than XML and faster for parsing. 


## Markdown

Markdown is a lightweight markup language that was started in 2004.  Markdown has simpler syntax rules than HTML and is becoming popular recently because Github and other leading companies support it. Markdown can be
easily converted to HTML by a parser for web display. 

The drawback of Markdown is their syntax is minimum, which means you only have a subset of what's available in HTML to work with in Markdown. 

There are tools to convert between HTML and Markdown. An example is [pandoc](http://www.pandoc.org). 


## Conclusion 

So what are the main differences and similarities among the above five formats?

* All five formats are human readable and can be hand-crafted using a text editor such as Notepad++. 

* HTML, XHTML, and Markdown are markup languages and they are used with the intention to be presented on the web. In other words, the target "consumer" of these markup languages is a web browser. Markdown is the lightweight version, HTML is the standard version, and XHTML is the XML-ized version of HTML.  

* XML and JSON are data exchange formats. The main "consumers" of XML and JSON are Application Programming Interfaces (API). For example, when you use Google's popular [geocoding API](https://developers.google.com/maps/documentation/geocoding/intro#Geocoding) to retrieve info about an address's geographic coordinates, you are working with JSON data or XML data. 


