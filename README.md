# Dokku Buildpack: nginx

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

You can override the nginx root via setting the `NGINX_ROOT` environment variable. This should be a relative path in your repository (for example `dokku config:set <app> NGINX_ROOT=_site` if you are deploying a Jekyll site).

You may completely override the built-in nginx config by placing an `app-nginx.conf.sigil` file in the root, modeled after our own [`conf/app-nginx.conf.sigil`](https://github.com/dokku/buildpack-nginx/blob/master/conf/app-nginx.conf.sigil). This will be used inside of the container, and not by the host Dokku instance. See the [sigil project](https://github.com/gliderlabs/sigil) for more information concerning the sigil format.

## Credits and License

`buildpack-nginx` is licensed under the CC0 1.0 Universal license and has been informed by many similar projects on the web.

[Florian Heinemann](http://twitter.com/TheSumOfAll/)
