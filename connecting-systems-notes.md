# HTTP

## Brief History

Hypertext - text displayed on computer displays with hyperlinks to other texts.

These hypertext documents are written in HTML and are exchanged using a certain protocol, HTTP (Hypertext Transfer Protocol).

HTTP/0.9 was simple, having only one command, "GET", this would retrieve the HTML of a page a user requests using its domain name/ip address[^1].

HTTP/1.0 improved on HTTP/0.9 by being more versatille. Browsers now had more to go off:
- a status code was prepended to a response a browser received, so that it could act accordingly
- **HTTP Headers** could be included in requests and responses, this included metadata, see the following example:

Typing a URL into the address bar causes your browser to send a request that looks similar to:
```
GET /tutorials/other/top-20-mysql-best-practices/ HTTP/1.1
Host: code.tutsplus.com
User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Keep-Alive: 300
Connection: keep-alive
Cookie: PHPSESSID=r2t5uvjq435r4q7ib3vtdjq120
```
The top line is the request line[^2], the others are HTTP headers. The browser will then receive a response that looks like:
```
HTTP/1.x 200 OK
Transfer-Encoding: chunked
Date: Sat, 28 Nov 2009 04:36:25 GMT
Server: LiteSpeed
Connection: close
X-Powered-By: W3 Total Cache/0.8
Content-Type: text/html

<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```
The first line is the status line containing one of the codes Kevin mentioned in his talk. Then there will be a block of HTTP headers followed by a blank line which is followed by the HTMl. 

The "Content-Type" header field now allowed documents other than HTML to be transferred. Above in the HTML we can see an IMG tag, after the iniial request the browser parses the HTML file and makes additional requests. For the above we have the following request and response:
```
GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(image content)
```

Other features were added experimentally to gauge their popularity (HTTP is extensible), for example creating your own header, as long as a server knew about this new header you could add new functionality. For example, the "Set-cookie" header overcomes the fact that HTTP is stateless (there is no link between requests), and so context can be added to a request - so shopping baskets can work!

But there were no standards which caused comtability issues, the solution would be to create a standard, and that is what HTTP/1.1 was.

## HTTP/1.1

HTTP/1.1 introduced new features yet again, including: support for multiple languages, a "Host" header was added which allows the same IP address to hold multiple domains (collocation). These all lead to the following four major improvements:
- **Efficient use of IP addresses**
- **Faster responses** - Connections could be reused, i.e. a browser could send multiple requests over a persistent connection. Dynamically generated pages responded faster due to "chunked encoding" which allows a response to be sent before its length is known, an obvious use case would be for video streaming.
- **Bandwidth saving** due to cache support, this is where a cache stores the response of a HTTP request and reuses it for subsequent requests, this will also lead to faster responses.

Recall that TCP was reliable and UDP was fast, for this reason HTTP uses TCP. To initially establish a TCP connection several round trips are required, in HTTP/1.0 this was done for each request/response pair, in HTTP/1.1 pipelining, and persistant connections were added:
- **Pipelining** - This is when multiple requests are sent over the same TCP connection without waiting for the responses in between, though only idempotent methods can be used.
- **Persistent Connections** - TCP connections actually perform better after time, they become "warm connections" and so connections that remain open have speed advantages. HTTP/1.1 included a "Keep-alive" header to specify a minimum time a TCP connection should be open for, this overrides the default time for which an idle connection will be closed.
**Note** - The default behaviour in HTTP/1.1 is a persistent connection, but it was still possible in HTTP/1.0 using the "Connection" header.


## HTTP/1.1 Issues
- Persistent connections consume server resources whilst idling
- HTTP/1.1 is not superior in all cases: the protocol itself is more complicated and so requires approximately 3-5x as much code compared to 1.0, this comes from needing to deal with all the headers introduced.[^3]



[^1]: Recall that DNS is the "phonebook" of the internet, each device connected to the internet has its own IP address (IPv4 is 32 bit and IPv6 is 128 bit so we won't run out). So when you type in a domain, the first call goes to a DNS solver.
[^2]: The format is "method path protocol", here method = GET, path = URL, protocol = HTTP/1.1
      The user is **always** responsible for creating a request to a server
[^3]: Supposedly, you could build a bare-bones HTTP/1.0 client in ~20 lines of code.
