Complete web server for Symfony 4 / 5 dev
=========================================

Based on [analogic/symserver](https://github.com/analogic/symserver)
(Debian trixie, s6-overlay v3), only the nginx config differs.

- PHP 7.4 (packages.sury.org)
- nginx + nchan (`/_sub/<channel>` websocket/SSE, `/_pub/<channel>` from localhost only)
- crontab (logrotate and other...)
- ssmtp (crontab errors sending)
- incrond (for sending spooled emails)

Symfony compatibility
---------------------

nginx serves `/var/www/public` with front controller `index.php` (Symfony Flex layout).

| Symfony   | Works | Note                                              |
|-----------|-------|---------------------------------------------------|
| 2.x, 3.x  | no    | `web/app.php` layout, use `analogic/symserver`    |
| 4.x       | yes   | 4.4 LTS recommended                               |
| 5.x       | yes   | 5.4 LTS recommended                               |
| 6.x, 7.x+ | no    | requires PHP >= 8.0.2 / 8.2                       |

```
$ docker run --name sym4server \
      -v /symfony/project/dir:/var/www \
      -v /data/logs:/var/log/nginx \
      analogic/sym4server
```
