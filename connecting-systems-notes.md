# HTTP 1.1

## Brief History

Hypertext - text displayed on computer displays with hyperlinks to other texts.

These hypertext documents are written in HTML and are exchanged using a certain protocol, HTTP (Hypertext Transfer Protocol).

HTTP/0.9 was simple, having only one command, "GET", this would retrieve the HTML of a page a user requests using its domain name/ip address[^1].

HTTP/1.0 improved on HTTP/0.9 by being more versatille. Browsers now had more to go off:
- a status code was prepended to a response a browser received, so that it could act accordingly
- **HTTP Headers** could be included in requests and responses, this included metadata

'''
def: grien(ed):
  dfeirfkmer
'''





[^1]: Recall that DNS is the "phonebook" of the internet, each device connected to the internet has its own IP address (IPv4 is 32 bit and IPv6 is 128 bit so we won't run out). So when you type in a domain, the first call goes to a DNS solver.
