# heroku-buildpack-nginx

This is the official dokku buildpack for static websites, powered by nginx.

## Usage

All static files that you want to serve should be in the root directory of your repository. No need to use a separate `www` folder. `buildpack-nginx` will automatically download the buildpack, download NGINX, compile it, and install it. The next time you push your project, the buildpack will reuse the precompiled binaries.

### Dokku

To trigger detection of this buildpack you need to add a dotfile:

Add an *empty* file called `.static` to your root directory of your web project (regardless if you use a custom value for NGINX_ROOT)

### Heroku

Heroku users can use this buildpack by running the following command:

```
heroku buildpacks:set https://github.com/dokku/buildpack-nginx.git
```

## Configuration

### Custom nginx root

You can override the nginx root via setting the `NGINX_ROOT` environment variable. This should be a relative path in your repository.

```shell
# where the app is named `static-app`
# and the root dir is _site
dokku config:set static-app NGINX_ROOT=_site
```

### Default to index for history routing

By default, this buildpack will 404 if a requested file is not found. For static sites that use the browser's history router to show the correct context, setting the `NGINX_DEFAULT_REQUEST` to a specific file will override this.

```shell
# where the app is named `static-app`
# and the desired default response is index.html
dokku config:set static-app NGINX_DEFAULT_REQUEST=index.html
```

### Custom nginx directives

You can configure following nginx directives via environment variables.

- `NGINX_WORKERS` : `worker_processes` directive
- `NGINX_WORKER_CONNECTIONS` : `worker_connections` directive
- `NGINX_CLIENT_BODY_TIMEOUT` : `client_body_timeout` directive
- `NGINX_CLIENT_MAX_BODY_SIZE` : `client_max_body_size` directive (in MB)

```shell
# where the app is named `static-app`
dokku config:set static-app NGINX_WORKERS=4 \
                            NGINX_WORKER_CONNECTIONS=1024 \
                            NGINX_CLIENT_BODY_TIMEOUT=5 \
                            NGINX_CLIENT_MAX_BODY_SIZE=1
```

### Custom nginx config file

You may completely override the built-in nginx config by placing an `app-nginx.conf.sigil` file in the root, modeled after our own [`conf/app-nginx.conf.sigil`](https://github.com/dokku/buildpack-nginx/blob/master/conf/app-nginx.conf.sigil). This will be used inside of the container, and not by the host Dokku instance. See the [sigil project](https://github.com/gliderlabs/sigil) for more information concerning the sigil format.

### Custom MIME types

Files will be served with a `Content-Type` according to a list of supported MIME types at [`conf/mime.types`](https://github.com/dokku/heroku-buildpack-nginx/blob/master/conf/mime.types). If you need to serve files of a MIME type not included in the list, you can provide your own `mime.types` file in the root.

## Credits and License

`buildpack-nginx` is licensed under the CC0 1.0 Universal license and has been informed by many similar projects on the web.

[Florian Heinemann](http://twitter.com/TheSumOfAll/)
