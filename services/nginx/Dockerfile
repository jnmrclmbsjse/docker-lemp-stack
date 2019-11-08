# Latest version of nginx image as of November 08, 2019
FROM nginx:1.17.5

# Copy nginx.conf to container Nginx configuration folder
COPY ./configuration/nginx.conf /etc/nginx/nginx.conf

# Mark these directories as volumes to be declared on docker-compose
VOLUME ["/var/www", "/etc/nginx/conf.d", "/var/log/nginx"]

# Set this as working directory
WORKDIR /var/www

# Default container command
CMD ["/usr/sbin/nginx"]
