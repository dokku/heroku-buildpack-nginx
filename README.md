# NGINX Buildpack for Dokku - Hosting static pages
This buildpack has been successfully run on Digital Ocean instances of Ubuntu 14.04 (Status: Jan 2015). It might also work with different configurations.

## Purpose
`buildpack-nginx` provides a simple, low overhead way of hosting static pages and websites on Dokku. Just add the `.env` and `.static` file to the root directory of your website as described below.

## Usage
1. Add a file with the name `.env` in the root of your directory with the following content: `export BUILDPACK_URL=https://github.com/florianheinemann/buildpack-nginx.git`
2. Add another, *empty* file called `.static` to your root directory of your web project. It signals that this buildpack shall be used
3. Push your project to Dokku

All static files that you want to serve should be in the root directory of your repository. No need to use a seperate `www` folder. `buildpack-nginx` will automatically download the buildpack, download NGINX, compile it, and install it. The next time you push your project, the buildpack will reuse the precompiled binaries. 

## NGINX CONFIGURATION
Override default configuration by adding `nginx.conf.erb` in the root directory

## Credits and License
`buildpack-nginx` is licensed under the CC0 1.0 Universal license and has been informed by many similar projects on the web

[Florian Heinemann](http://twitter.com/TheSumOfAll/)
