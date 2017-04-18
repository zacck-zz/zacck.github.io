---
  layout: post
  title: Updating letsencrypt on Heroku
  tags: [heroku,ssl,letsencrypt,certbot]
  categories:
---

So it has been a 90 Days!  
Let me clarify it has been 90 days of free ssl from letsencrypt using certbot.

We run into our first issue. I need to update my ssl certificates for my heroku app.
First of I should mention this was triggered by an email from letsencrypt telling
me my certificate would expire today.

Here are my notes


first off lets renew our certificates by running

`sudo certbot -d mydomain.com`

This will give us a screen asking us where we want to reinstall the certificate or renew & replace the certificate.

Since our current certificate is expiring we go with option 2

This will renew and save our new cerficate in the location of the old one

in my case in

`etc/letsencrypt/live/mydomain.com/fullchain.pem`

and

`etc/letsencrypt/live/mydomain.com/privkey.pem`

LetsEncrypt will now prompt you to set up your domain to respond with and answer

~~~~
Make sure your web server displays the following content at
http://www.mydomain.com/.well-known/acme-challenge/xxxxxxxxxxxx-yyyy.zzzzzzzzzzzzzzzzzzz before continuing:
xxxxxxxxxxxx-yyyy.zzzzzzzzzzzzzzzzzzz
If you don’t have HTTP server configured, you can run the following
command on the target server (as root):
mkdir -p /tmp/certbot/public_html/.well-known/acme-challenge
cd /tmp/certbot/public_html
printf “%s” Gm35kFLiXnNtKT9OAOG_KPZvqMmYYAZU6DN-QRoGclg.s2I4ZV9Ne2CNtczlqXV9uw1ZdB5OSypG_cIdiuT7BwI > .well-known/acme-challenge/Gm35kFLiXnNtKT9OAOG_KPZvqMmYYAZU6DN-QRoGclg
# run only once per server:
$(command -v python2 || command -v python2.7 || command -v python2.6) -c \
“import BaseHTTPServer, SimpleHTTPServer; \
s = BaseHTTPServer.HTTPServer((‘’, 80), SimpleHTTPServer.SimpleHTTPRequestHandler); \
s.serve_forever()”
Press ENTER to continue
~~~~


#**Make Sure to to ship this to your app before pressing enter in the step above**
I use express.js for serving my application on heroku and hence i can use this snippet.

~~~~
app.get('/.well-known/acme-challenge/:content', function(req, res) {
  res.send('xxxxxxxxxxxx-yyyy.zzzzzzzzzzzzzzzzzzz')
})
~~~~

At this point you can press enter and letsencrypt will show you a congratulations message on on loading your certificate.

Anothet 90 Days!....

I should likely Automate this using system timers refer @mralanorth

&#x1f61d;
