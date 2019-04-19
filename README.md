# Proxy Server

Multi-threaded HTTP proxy server using Python socket programming.

## Features

* Clients can send HTTP GET and POST requests to the proxy server which either sends requests to the destination IP or any local server.
* The proxy server caches upto three responses whose URL has been requested more than 3 times in 5 minutes.
* Certain domains are blacklisted. These are stored in CIDR format in the file `proxy-server/proxy/blacklist.txt`.
* Blacklisted domains can only be accessed by certain users using Basic Access Authentication.

## Running the code

### Proxy server

The proxy server runs on port 20100.

```shell
cd proxy-server
python3 main.py
```

To serve local files, run local servers in the port range 20101 to 20200:

```shell
cd server
python2 server.py 20101 20200
```

### Client

Curl requests can be sent from any port in the range 20000-20099 to the proxy server at port 20100. Only HTTP requests are supported - not HTTPS.

To request a certain URL:

```shell
curl --proxy 127.0.0.1:20100 --local-port 20000-20099 <url>
```

To request blacklisted domains, username and password must be provided:

```shell
curl --proxy 127.0.0.1:20100 --local-port 20000-20099 -u username:password <url>
```

To retrieve any file using a local server:

```shell
curl --proxy localhost:20100 --local-port 20000-20099 -X GET localhost:10000/server.py
```
