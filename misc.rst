Asynchronous ICE
----------------

Ice is inherently an asynchronous middleware platform that simulates
synchronous behavior for the benifit of applications. When an Ice application
makes a synchronous twoway invocation on a proxy for a remote object, the
operation's in parameters are marshaled into a message that is written to a
transport, and the calling thread is blocked in order to simulate a
synchronous method call.
  
A programmer indicates a desire to use an asynchronous model(AMI, AMD, or
both) by annotating Slice definition with metadata. 

Synchronous invocation methods are always generated in a proxy; specifying AMI
annotation merely adds synchronous invocation methods. 

Asynchronous Method Dispath (AMD)
---------------------------------

Asynchronous Method Dispath (AMD), the server-side equivalent of AMI,
addresses this scalability issue. Using AMD, a server can receive a request
but then suspend its processing in order to release the dispatch thread as
soon as possible. When processing resumes and the results are available, the
server sends a response explicitly using a callback object provided by the Ice
runtime. AMD is transparent to client.

In practical terms, an AMD operation typically queues the request data. In
this way, the server minimizes the use of dispatch threads and become capable
of efficiently supporting thousands of simultaneous clients.

Google Code with Mercurial
==========================

Google Code
-----------
- clone google code to local repository with::

  hg clone https://project-name.googlecode.com/hg/    

Mercurial
---------

Mercurial does not have the Index concept as git, so you could use *hg add* to
add a new file to the repo, but /hg add/ is not appropriate to be used again
when you update a file. In reverse, you should use *hg commit <filename>*
directly when update a file.
    
GBK 0x5C and json
=================

0x5C is the ASCII encoding character '/', which in most cases, is used as escape
charater. Combine with following characters, it tells the compiler or library to
converting them to certain character when processing.

But unfortunately, 0x5C is a valid byte of a character in GBK encoding. So if
you have a GBK charater with 0x5C as one part, then you may have trouble when
processing it with libraries support escape character. For example the
json_encode/json_decode implementation in json libraries.

So, basically, it is more safer to use utf-8 encoding when you're willing to use
json_encode/json_decode.






