FROM debian:jessie

MAINTAINER William Li "williamli@bbi.io"

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
  && echo "deb http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list \
  && apt-get update \
  && apt-get install -y ca-certificates nginx gettext-base \
  && rm -rf /var/lib/apt/lists/*

# maps /var/www to /usr/share/nginx/html
RUN ln -sf /usr/share/nginx/html /var/www

# forward request and error logs to docker log collector
#RUN ln -sf /dev/stdout /var/log/nginx/access.log \
#  && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
