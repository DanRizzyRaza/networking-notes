# HTTP 1.1

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
The top line is the request line, the others are HTTP headers. The browser will then receive a response that looks like:
```
HTTP/1.x 200 OK
Transfer-Encoding: chunked
Date: Sat, 28 Nov 2009 04:36:25 GMT
Server: LiteSpeed
Connection: close
X-Powered-By: W3 Total Cache/0.8
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<!-- ... rest of the html ... -->
```

The "Content-Type" header field now allowed documents other than HTML to be transferred.





[^1]: Recall that DNS is the "phonebook" of the internet, each device connected to the internet has its own IP address (IPv4 is 32 bit and IPv6 is 128 bit so we won't run out). So when you type in a domain, the first call goes to a DNS solver.
