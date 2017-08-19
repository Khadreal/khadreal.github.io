---
layout: post
title: "How to Install Let's Encrypt HTTPS on Amazon EC2 Instance Ubuntu"
date: 2017-08-19 16:08:41 +0100

permalink: /how-to-install-lets-encrypt-https-on-amazon-ec2-instance/
categories:
---

![How to Install Let's Encrypt HTTPS on Amazon EC2 Instance Ubuntu]({{ site.url }}/assets/image/let-encrypt.jpg)


Let’s Encrypt is a free, automated, and open Certificate Authority which provides free SSL certificates.
It makes deploying SSL certicate for your web server a relatively straight forward process.

Shameful admission: I’m adapting this post from step-by-step notes taken during my own install over this week, so please excuse any indistinct details and certainly leave feedback if anything is unclear so I can make improvements!

Let's get started.

**Step #0: Prerequites**

Make sure you have opened up ports 80 (HTTP) and 443 (HTTPS) in your instance security group to public.

A user with sudo privileges.

Point your domain to your Amazon EC2 Elastic IP

**Step #1: Installation**

Run the command below

`$ sudo apt-get update`

`$ sudo apt-get install software-properties-common`

`$ sudo add-apt-repository ppa:certbot/certbot`

`$ sudo apt-get update`

`$ sudo apt-get install python-certbot-apache` 

`$ sudo certbot --apache`

**Step #2: Edit Conf files**

Open your apache2.conf file

`$ sudo nano etc/apache2/sites-available/000-default-ssl.conf `
`<VirtualHost *:443>`

    ServerName example.com
    ServerAdmin webmaster@example.com
    RewriteEngine on
    DocumentRoot "/var/www/html/"
	SSLCertificateFile /etc/letsencrypt/live/example.com/fullchain.pem
	SSLCertificateKeyFile /etc/letsencrypt/live/example.com/privkey.pem
	Include /etc/letsencrypt/options-ssl-apache.conf
`</VirtualHost>`

If your installation was successful the last 3 lines in your conf files is auto generated

**Step #3: Restart your Server**

`$ sudo service apache2 restart`

**Step #4: Enable auto renewal (Optional)**
$ sudo crontab -e

Your text editor will open the default crontab which is a text file with some help text in it. Paste in the following line at the end of the file, then save and close it:

`15 3 * * * /usr/bin/certbot renew --quiet`


The 15 3 * * * part of this line means "run the following command at 3:15 am, every day". You may choose any time.

The renew command for Certbot will check all certificates installed on the system and update any that are set to expire in less than thirty days. --quiet tells Certbot not to output information nor wait for user input.