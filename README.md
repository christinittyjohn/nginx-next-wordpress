### nginx-nextjs-wordpress

An example setup to host a nextjs app along with wordpress with nginx.
Wordpress is available at `/content`.

### wordpress

[Site](http://3.110.51.92/content)<br>
[Admin panel](http://3.110.51.92/wp/wp-admin/)

- uses the official wordpress docker [image](https://hub.docker.com/_/wordpress/)
- wodpress site is available at `/content`
- wordpress admin panel can be accessed at - `/wp/wp-admin`
- [extra wordpress config changes](https://github.com/christinittyjohn/nging-next-wordpress/blob/main/docker-compose.yml#L23)
- `WP_HOME` is set to `host-ip/content`, this ensures that the wordpress site is hosted at /content
- `WP_SITEURL` is set to `host-ip/wp`, this allows us to identify and proxy wordpress client's asset requests. As a sideeffect this also changes the path of the admin panel, instead of `/wp-admin` it changes to `WP_SITEURL/wp-admin`

### nextjs

[Next.js app](http://3.110.51.92)

- the starter nextjs app is containerized on top of `node:16-alpine` and runs at port `3000`
- all paths apart from `/content\w*` and `/wp/*` will be proxied to the next server

### nginx

- [config](https://github.com/christinittyjohn/nging-next-wordpress/blob/main/proxy/nginx.conf)
- uses the official nginx docker [image](https://hub.docker.com/_/nginx/).
- multiple `location` directives are used to create proxy rules.
- Host header is set using `proxy_set_header` is required, which wordpress uses to handle requests.
