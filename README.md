c9-tor-scraper-fun
==================

Attempting a cloud-based onion-routing webscraper (python) 

as per https://deshmukhsuraj.wordpress.com/2015/03/08/anonymous-web-scraping-using-python-and-tor/

#### Install Pythonlibs + Tor
```
$ sudo pip install pysocks

$ sudo pip install requests

$ sudo apt-get update

$ sudo apt-get install tor
```
Since we're on c9 we'll try to use <b>PORT 8081 or 8082</b> instead -
(See also https://c9.io/blog/multiple-ports/)
```
$ tor --SOCKSPort 8082
```
leave that running
```
$ netstat -tupln
```
will show what ports are open aka <b>"tuple-in"</b>

Now you can run the code:
```
$ python tor-ip-test.py

# 51.255.33.0
```

### Changing Exit Nodes 

I was expecting the result of `python tor-ip-test.py` to change each time I ran it, but it remains the same.

Restarting `tor` process changes the IP, but there must be better.

As usual, grepping through the `man` page doesn't get the answer as fast as googling it - http://stackoverflow.com/questions/6216653/how-to-let-tor-change-ip-automatically
says the IP should change every 10 minutes at most, but what if thats NOT GOOD ENOUGH

add `MaxCircuitDirtiness 15` to the bottom of `etc/tor/torrc` for refresh every 15s

### IT WORKS

```
// 37.187.129.166
// 89.234.157.254
// 62.210.37.82
// 46.101.98.208
```

Bonus: Those 4 above were all labeled "Anonymous Proxy" at http://geoip.com. 


Cool!