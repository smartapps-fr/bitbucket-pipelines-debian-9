[![Travis Build Status](https://travis-ci.org/smartapps-fr/bitbucket-pipelines-debian-9.svg)](https://travis-ci.org/smartapps-fr/bitbucket-pipelines-debian-9) [![Microbadger badge](https://images.microbadger.com/badges/image/smartapps/bitbucket-pipelines-debian-9.svg)](https://microbadger.com/images/smartapps/bitbucket-pipelines-debian-9)

# bitbucket-pipelines-debian-9(-php-mysql)

[Bitbucket Pipelines](https://bitbucket.org/product/features/pipelines) [Docker](https://www.docker.com/) image based on [Debian 9.0 _Stretch_](https://www.debian.org/releases/stretch/) with [PHP](http://php.net/)/[MySQL](https://www.mysql.com) (and more !)

More help in Bitbucket's [Confluence](https://confluence.atlassian.com/bitbucket/bitbucket-pipelines-beta-792496469.html)

Docker image at [smartapps/bitbucket-pipelines-debian-9](https://hub.docker.com/r/smartapps/bitbucket-pipelines-debian-9/) (no `CMD` as it is overriden by *Pipelines*)

## Packages installed

 - `php-apcu`, `php-bcmath`, `php-cli`, `php-curl`, `php-gd`, `php-geoip`, `php-gettext`, `php-imagick`, `php-intl`, `php-json`, `php-mbstring`, `php-mcrypt`, `php-memcached`, `php-mysql`, `php-sqlite3`, `php-xdebug`, `php-xml`, `php-xmlrpc`, `php-zip`, `memcached`, `imagemagick`, `openssh-client`, `curl`, `gettext`, `zip`, `git`, `subversion`
 - [Perl](https://www.perl.org/) 5.24
 - [Python](https://www.python.org/) 2.7 & 3.5
 - [MariaDB](https://mariadb.org/) 10.1 (mostly compatible with [MySQL](https://www.mysql.com/) 5.6) (user `root:root`)
 - [PHP](http://www.php.net/) 7.0 (default), 7.1 & 7.2 (use interpreters `/usr/bin/php7.0`, `/usr/bin/php7.1` & `/usr/bin/php7.2`, as [described here](https://pehapkari.cz/blog/2017/03/27/multiple-php-versions-the-easy-way/))
 - [Ruby](https://www.ruby-lang.org/) 2.3
 - [Node.js](https://nodejs.org/) 8.x LTS (you can use [`n`](https://github.com/tj/n) to interactively manage your Node.js versions)
 - Latest [Composer](https://getcomposer.org/), [Gulp](http://gulpjs.com/), [Webpack](https://webpack.github.io/), [Mocha](https://mochajs.org/), [Grunt](http://gruntjs.com/), [PHPUnit](https://phpunit.de/), [Codeception](https://codeception.com/), [Yarn](https://yarnpkg.com/), [n](https://github.com/tj/n)

## Sample `bitbucket-pipelines.yml`

```YAML
image: smartapps/bitbucket-pipelines-debian-9
pipelines:
  default:
    - step:
        script:
          - service mysql start
          - mysql -h localhost --user=root --password=root -e "CREATE DATABASE test;"
          - composer config -g github-oauth.github.com XXXXXXXX
          - composer install --no-interaction --no-progress --prefer-dist
          - npm install --no-spin
          - gulp
```
