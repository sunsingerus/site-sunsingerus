---
ID: 9
post_title: >
  HowTo Setup HTTPS with
  https://letsencrypt.org/
author: sunsingerus
post_excerpt: ""
layout: post
permalink: >
  https://sunsingerus.com/howto-setup-https-with-https-letsencrypt-org/
published: true
post_date: 2018-01-20 16:19:12
---
<h5>Introduction</h5>

<a href="https://letsencrypt.org/" rel="noopener" target="_blank">Let's Encrypt</a> is a free, automated, and open Certificate Authority. It provides free of charge SSL certificates to setup HTTPS on a site.
The best way to simplify and automate SSL certificates management is to use <a href="https://certbot.eff.org/" rel="noopener" target="_blank">certbot</a> - special tool for communication with Let's Encrypt API.

Suppose we have NGINX running on CentOS or Ubuntu system. Let's automate certificates management with certbot.

<strong>IMPORTANT</strong> Let's Encrypt issues certificates with <strong>90 days</strong> valid period, so certificate renewal procedure is mandatory. Also we'd like to automate it.
<h5>Certbot Installation</h5>
Firts of all, let's install certbot

<code>Ubuntu</code>
<pre>
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python-certbot-nginx 
</pre>

<code>CentOS</code>
<pre>
sudo yum -y install yum-utils
sudo yum-config-manager --enable rhui-REGION-rhel-server-extras rhui-REGION-rhel-server-optional
sudo yum install certbot-nginx
</pre>

<code>Latest version from developers</code>
Latest version can be required in case you met with the following error message with certbot installed from repos: <strong>"Client with the currently selected authenticator does not support any combination of challenges that will satisfy the CA."</strong>
<pre>
wget https://dl.eff.org/certbot-auto
chmod a+x ./certbot-auto
./certbot-auto --help
</pre>

<h5>Obtain Certificates and Configure NGINX</h5>
Run
<pre>
./certbot-auto --nginx
</pre>
Answer some tools asked by the tool. That's all. Really. Certificates obtained, NGINX configured.
Certbot adds the folling lines into NGINX configuration
<pre>
listen 443 ssl; # managed by Certbot
ssl_certificate /etc/letsencrypt/live/sunsingerus.com/fullchain.pem; # managed by Certbot
ssl_certificate_key /etc/letsencrypt/live/sunsingerus.com/privkey.pem; # managed by Certbot
include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
</pre>
and it also adds redirect from HHTP to HTTPS
<pre>
return 301 https://$host$request_uri; # managed by Certbot
</pre>

<h5>List installed certificates</h5>
<pre>
./certbot-auto certificates
</pre>

<h5>Renew Certificates</h5>
<pre>
./certbot-auto renew
</pre>
That's all. Exactly as the doc says "renew is suitable (and designed) for automated use, to allow your system to automatically renew each certificate when appropriate. Since renew only renews certificates that are near expiry it can be run as frequently as you want - since it will usually take no action."

<h5>Automate Certificates Renewal</h5>

Place renewal script into <core>/etc/cron.daily/</code> folder
<pre>
#!/bin/sh
/root/certbot-auto renew
</pre>

<h5>Renew Hooks</h5>
In case we need some complex action on renewal procedure we can use renew pre and post hooks
<pre>
certbot renew --pre-hook "service nginx stop" --post-hook "service nginx start"
</pre>