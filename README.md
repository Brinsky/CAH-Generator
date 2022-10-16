CAH-Generator (brinsky@'s fork)
=============

> *Uses imagemagick to create Cards Against Humanity images for printing on actual cards through a print studio.*

I forked my version from https://github.com/zaffudo/CAH-Generator, which was hosted on http://mywastedlife.com/CAH but seems to have developed some bit rot (e.g. [missing text](https://github.com/zaffudo/CAH-Generator/issues/14)) as of October 2022.

## Setup

Here are my rough notes for installing Apache + PHP and running this site out of `/srv/http` on Arch Linux: 

1. Install the relevant packages:
    - `apache` (i.e. https://wiki.archlinux.org/title/Apache_HTTP_Server#Installation and [#Configuration](https://wiki.archlinux.org/title/Apache_HTTP_Server#Configuration))
    - `php-fpm` (and follow https://wiki.archlinux.org/title/Apache_HTTP_Server#Using_php-fpm_and_mod_proxy_fcgi)
    - `perl`
    - `imagemagick`

2. Prepare the server and website (note - you will need to run most commands as root):
    - Run `chown -R http:http /srv/http` to make Apache's `http` user the owner of the `/srv/http` directory
    - Clone this repository under `/srv/http` (so `/srv/http/CAH-Generator`)
    - Acquire HelveticaNeue font sources and place them in `/srv/http/CAH-Generator/fonts/`
        - The specific requirement is to have a file named `HelveticaNeueBold.tff` in that folder
    - Run `systemctl start httpd.service php-fpm.service` to start Apache and PHP FPM (you could also do `enable --now` instead of `start` to always run them on startup) 
    - Access http://localhost/CAH-Generator/index.html

## Misc

- My fonts came with names of the form `HelveticaNeue-Bold.ttf`, so I installed/used the `perl-rename` package to rename them:
    - `perl-rename 's/(HelveticaNeue)-?(\w+)\.(\w*)/$1$2\.$3/' /srv/http/CAH-Generator/fonts/*`
- `tail -f /var/log/httpd/error_log` was useful for debugging Apache/PHP errors
