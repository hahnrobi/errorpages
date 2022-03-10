# errorpages
Simple error pages for web servers.

## What is it for?
If you want to have some customized error messages on your webserver, you can use this repo as a good starting point. It has all the configuration to get you up and running.

> The configuration files now only for NGINX. Apache version is on it's way.

## Features
Customized, responsive 21th century looking error pages, which can be easily customized. It contains an includable configuration file, you can include it to your existing sites/virtualhosts with a single line and use it where you would like.

You can specify specific pages with a completely custom template and can use a generic one for errors which doesn's explicitly have a dedicated error pages. This is done with the NGINX ssi directice. You can also use this feature to make the generic page react to different error codes differently.

Autoreload feature, which can be used the automatically reload the page in the browser, if the page will be online quickly. For example 502 errors while PHP FPM starting up.

## Important
**This project is still work in progress.**

## Set up
The default location for the error html pages is /var/www/_errors.
Copy the `4xx.html` and `5xx.html` files there and also the generic error file. For example with NGINX: copy `_error_nginx.html` and rename it to `_error_nginx.html`.
The initial directory content of the _errors folder would be:
- 403.html
- 404.html
- ...
- _error.html

The `conf.d folder` contains the NGINX configuration files what should be copied to your NGINX `conf.d` folder. The error-pages.conf file has an `.optional` suffix, that way if you use autoimport in NGINX it will be not imported automatically in the `http` block. It would be unusable in the `http` block.

To actually use the configuration file, edit one of your site configuration file and add the following line in the `server` block:
`include conf.d/error-pages.conf.optional;`

A very-very basic example site configuration file:
> sites-available/mysite
```
server {
    listen 80;
    server_name: mysite.com;
    root /var/www/html/mysite.com;
    include conf./error-pages.conf.optional;
}
```

## Other info
If you have any suggestions or issues, feel free to use the issues tab or make a PR.
