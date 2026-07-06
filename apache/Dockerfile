FROM debian:stable-slim

# Install Apache and ModSecurity
RUN apt update && apt install -y \
    apache2 \
    libapache2-mod-security2 \
    openssl

# Enable required Apache modules
RUN a2enmod proxy proxy_fcgi rewrite headers security2 env setenvif dir mime ssl

COPY ./config/security.conf /etc/apache2/conf-available/security.conf
COPY ./config/modsecurity-custom.conf /etc/apache2/mods-available/security2.conf
COPY ./ssl/certs/nextcloud.dalotech.cert /etc/ssl/certs/nextcloud.dalotech.cert
COPY ./ssl/private/nextcloud.dalotech.key /etc/ssl/private/nextcloud.dalotech.key

# Enable the hardening config
RUN a2enconf security

EXPOSE 80 443

# Start Apache in the foreground
CMD ["apachectl", "-D", "FOREGROUND"]
