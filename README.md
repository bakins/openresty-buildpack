# OpenResty buildpack

This is an heroku style buildpack for running openresty.  It varies from various others I have found in that it does not bundle binaries in the repo. It is also written almost entirely in shell.

# start-nginx and nginx.slt
You should include your nginx configuration in a file `nginx.slt` in the root of your project. [Simple Lua Template](https://github.com/henix/slt2) is used to render this to `nginx.conf`
The `start_nginx` script is used to start nginx. It handles the template rendering as well as setting some environment variables. Note, you should set `daemon off` in your nginx config.

# OPENRESTY file
each project should include an `OPENRESTY` file. This file is actually bash and is used by the `compile` script. It supports two directives, as well as normal shell:

* `openresty 'version'` or `openresty 'version' 'mirror' - specify the version of openresty to use. This currently must be before any `rock` stanzas.  The binaries of openresty are stored in a mirror with the path `$MIRROR/openresty-$VERSION.tar,gz` you can pass the mirror as the second argument to openresty
* `rock 'name'` or ``rock 'name' 'version'` or `rock 'url'`- install a Lua rock, either by name, which will use the standard luarocks mirror, or by url.

# template variables

A few helper variables are included for use with the `nginx.slt`

* `LUA_PACKAGE_PATH` - the LUA_PATH fixed to use the vendored paths.
* `LUA_PACKAGE_CPATH` - the LUA_CPATH fixed to use the vendored paths.

These should be used in your templates like:

    lua_package_path "$prefix/lib/?.lua;#{= LUA_PACKAGE_PATH };;";
    lua_package_cpath "#{= LUA_PACKAGE_CPATH };;";


