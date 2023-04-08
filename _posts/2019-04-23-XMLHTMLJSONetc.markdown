---
layout: post
title:  "A peek into HTML, XML, XHTML, JSON, YML, and Markdown"
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

JSON is a lightweight data interchange format widely used on the web. JSON is part of Javascript. Because Javascript is a scripting language that can be embedded within HTML, you can directly use JSON in an HTML page. JSON was invented in 2002. 

JSON denotes data objects in key-value pairs and is gaining wide adoption because it is much simpler than XML and faster for parsing. JSON is a data-only format and does not permit adding comments in it. 

JSON is also a popular format for DevOp configurations and specifications. For example, you can use JSON to define [OpenAPI specification](https://en.wikipedia.org/wiki/OpenAPI_Specification). 

## YAML (or YML)

YAML stands for Yet Another Markup Language. YAML is a data serialization language and it is more human readable than XML and JSON. YML allows you to put comments in it. YML is widely used in pipeline configurations such as in GitLab CI configuration. You can also use YML to define OpenAPI/Swagger specification. 


## Markdown

Markdown is a lightweight markup language that was started in 2004.  Markdown has simpler syntax rules than HTML and is becoming popular recently because Github and other leading companies support it. Markdown can be easily converted to HTML by a parser for web display. 

The drawback of Markdown is their syntax is minimum, which means you only have a subset of what's available in HTML to work with in Markdown. 

There are tools to convert between HTML and Markdown. An example is [pandoc](http://www.pandoc.org). 


## Conclusion 

So what are the main differences and similarities among the above formats?

* All the formats are human readable and can be hand-crafted using a text editor such as Notepad++. 

* HTML, XHTML, and Markdown are markup languages and they are used with the intention to be presented on the web. In other words, the target "consumer" of these markup languages is a web browser. Markdown is the lightweight version, HTML is the standard version, and XHTML is the XML-ized version of HTML.  

* XML and JSON are data exchange formats. The main "consumers" of XML and JSON are Application Programming Interfaces (API). For example, when you use Google's popular [geocoding API](https://developers.google.com/maps/documentation/geocoding/intro#Geocoding) to retrieve info about an address's geographic coordinates, you are working with JSON data or XML data. 
  
* YML is widely used for pipeline configurations and static site generator configurations. 

---------

Updates on April 7, 2023

I asked ChatGPT this question:
### Prompt: Compare HTML, XML, XHTML, JSON, YML, and Markdown.

### Following is ChatGPT's answer

HTML, XML, XHTML, JSON, YML, and Markdown are all different markup languages used for different purposes. Here is a brief comparison between them:

    HTML: HTML (Hypertext Markup Language) is a markup language used to create web pages. It is used to structure content, define headings, paragraphs, links, images, and other elements that make up a web page.

    XML: XML (Extensible Markup Language) is a markup language used for data exchange and storage. It is used to describe data and metadata and is commonly used in web services and APIs.

    XHTML: XHTML (Extensible Hypertext Markup Language) is a markup language similar to HTML, but it is stricter and follows the rules of XML. It is used for web pages that need to be more compliant with XML standards.

    JSON: JSON (JavaScript Object Notation) is a lightweight data interchange format that is easy to read and write for both humans and machines. It is commonly used to transmit data between a server and a web application, as well as for storing and exchanging data.

    YML: YML (YAML Ain't Markup Language) is a human-readable data serialization format that is often used for configuration files. It is commonly used in software development and system administration.

    Markdown: Markdown is a lightweight markup language used to format plain text. It is commonly used in documentation, readme files, and other places where simple formatting is required.

In summary, HTML and XHTML are used for creating web pages, XML is used for data exchange and storage, JSON is used for data transmission and exchange, YML is used for configuration files, and Markdown is used for simple formatting of plain text.


