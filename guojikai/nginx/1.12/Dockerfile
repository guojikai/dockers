FROM guojikai/alpine:3.6-dev

RUN apk update \
    && apk add ca-certificates nginx \
    # maps /var/www to /usr/share/nginx/html
    && ln -sf /usr/share/nginx/html /var/www
    # forward request and error logs to docker log collector
    # && ln -sf /dev/stdout /var/log/nginx/access.log \
    # && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]

