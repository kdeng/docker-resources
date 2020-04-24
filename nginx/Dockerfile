FROM nginx:alpine

ENV TZ Pacific/Auckland

COPY /nginx/api_gateway.conf /etc/nginx/
COPY /nginx/nginx.conf /etc/nginx/
COPY /nginx/api_conf.d/* /etc/nginx/api_conf.d/
COPY /nginx/html /usr/share/nginx/html

EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
