# NGINX Buildpack

**Note**: This has only been tested with [dokku](https://github.com/progrium/dokku) - it may not work elsewhere.

## Structure
* .nginx - File: its presence signals that this buildpack should be used
* www - Folder: holds all files to be served by nginx
* nginx.conf.erb - Optional File: overrides `conf/nginx.conf.erb`
* mime.types - Optional File: overrides `conf/mime.types`
* custom-build - Optional File: executes commands before build is finished. Note that this script does not run in the application root. To execute commands in the application root you must do `cd "$1"`.

## Environment Variables
* root - Optional: overrides root directory
