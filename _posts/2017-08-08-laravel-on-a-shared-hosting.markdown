---
layout: post
title: "Guide on how to Deploy Laravel 5 on shared hosting"
date: 2017-08-08 18:19:51 +0100

permalink: /guide-on-how-to-deploy-laravel-5-on-a-shared-hosting/
categories:
---

![Deploy Laravel on a Shared Hosting]({{ site.url }}/assets/image/laravel.jpg)

In this post, I'd like to show you how to deploy your Laravel 5 application, safe and secure on a shared hosting.

Am assuming you have **public_html** directory, for example

`/home/opeyemi/public_html`

Now, create a new directory at the same level as your **public_html**, for example

`/home/opeyemi/project`

After creating this project[or whatever you name the directory].

You can now transfer your Laravel 5 code to the newly created directory.

At this point, your application is still not accessible incase you tried to view on the browser.

To make your project accessible, the first step is to copy all contents inside the **/home/opeyemi/project/** folder to **/home/opeyemi/public_html/** .

Next step is to modify the **index.php** inside the **/home/opeyemi/public_html/**, find the following line of code
`
require __DIR__.'/../bootstrap/autoload.php';
$app = require_once __DIR__.'/../bootstrap/app.php';
`

Update the line of code to the correct paths as following

`
require __DIR__.'/../project/bootstrap/autoload.php';
$app = require_once __DIR__.'/../project/bootstrap/app.php';
`

After modifying the index.php file, don't forget to configure your application variables in **/home/opeyemi/project/.env**

Yes!! Everything should work fine now

P.S Dont' forget to copy the **.htaccess** to **/home/opeyemi/public_html**
