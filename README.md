# moudixtc/openresty
Docker image for [openresty](https://openresty.org/en/) based on Ubuntu 16.04 LTS.

# Tags
- [`latest` (*latest/Dockerfile*)](https://github.com/moudixtc/docker-openresty/blob/master/latest/Dockerfile)
- [`1.11.2.5`, (*1.11.2.5/Dockerfile*)](https://github.com/moudixtc/docker-openresty/blob/master/1.11.2.5/Dockerfile)

# Usage
The default command copies all the config files under the `NGINX_CUSTOM_CONF_DIR`, which defaults to `/nginx-conf`, to the openresty's config directory at `/usr/local/openresty/nginx/conf`. Therefore, mount your host directory that contains all the config files to override the default configuration.

1. Use docker's `--mount` flag
    ```bash
    docker run -d --mount type=bind,source=<CONFIG_DIR_ON_HOST>,destination=/nginx-conf,readonly moudixtc/openresty
    ```
1. or the traditional `-v` flag
    ```bash
    docker run -d -v <CONFIG_DIR_ON_HOST>:/nginx-conf:ro moudixtc/openresty
    ```
