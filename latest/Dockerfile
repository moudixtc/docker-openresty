FROM ubuntu:16.04

LABEL maintainer="Di Mou <moudi717@gmail.com>" \
      image="moudixtc/openresty:latest"

ARG dumb_init_version=1.2.0
ARG dumb_init_path=/usr/local/bin/dumb-init
ENV OPENRESTY_PREFIX=/usr/local/openresty
ENV PATH=${PATH}:${OPENRESTY_PREFIX}/luajit/bin \
    NGINX_CUSTOM_CONF_DIR=/nginx-conf

RUN apt-get update && \
    apt-get install -y curl && \
    mkdir -p ${NGINX_CUSTOM_CONF_DIR} && \
    curl -sSL -o ${dumb_init_path} https://github.com/Yelp/dumb-init/releases/download/v${dumb_init_version}/dumb-init_${dumb_init_version}_amd64 && \
    chmod +x ${dumb_init_path} && \
    curl -sSL https://openresty.org/package/pubkey.gpg | apt-key add - && \
    echo "deb http://openresty.org/package/ubuntu xenial main" >> /etc/apt/sources.list.d/openresty.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends openresty

ENTRYPOINT ["dumb-init", "--"]
CMD ["/bin/bash", "-c", "cp -r ${NGINX_CUSTOM_CONF_DIR}/* ${OPENRESTY_PREFIX}/nginx/conf/ && exec /usr/bin/openresty -g 'daemon off;'"]
