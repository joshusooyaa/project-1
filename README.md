Author: Josh Sawyer
Contact: jsawyer2@uoregon.edu

This is a simple server that responds to "GET" requests from the client side, therefore no other requests
are implemented, and an HTTP/1.0 404 Not Implemented is transmitted if other requests are sent.

The server accesses files using the docroot (the docroot is path to the directory the files exist in) - this 
can be changed using credentials-skel.ini. The port number is also changed through credentials-skel.ini.

pageserver.py - 
The server serves only .html and .css files. When a GET request is sent for a file that exists in the docroot
the server will first send a 200 code (implying a successful request) and then send the file that it found 
within the docroot. If there is a link to a css file, it will attempt to find it in the docroot as well (a
second request is sent for that css file) - if it is found, it'll link the css to the html, otherwise a 404
response is sent (in regards to the css file) and then the html file is displayed without the linked css. If
a request for just .css is sent, it'll display the raw css (given that the .css exists in the docroot (path)).

If a file does not exist, in which the client tried accessing, a 404 response is sent, implying the data
for this page wasn't found. Additionally, if a client sends a GET request with the string '..' or '~' 
a 403 response is sent implying that this is a forbidden request and the page cannot be accessed.

It can be run using 'make start' and you can stop it using 'make stop'
