# Latest version of MariaDB image as of November 08, 2019
# This service is MySQL but I took image from MariaDB since
# it is full-featured yet acts the same as MySQL
FROM mariadb:10.4.8

# Copy my.cnf to container MySQL configuration folder
COPY ./configuration/my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 644 /etc/mysql/conf.d/my.cnf

# Expose port to host
EXPOSE 3306

# Default container command
CMD ["mysqld"]
