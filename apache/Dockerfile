FROM debian:stable-slim

# Install Apache and ModSecurity
RUN apt update && apt install -y \
    apache2 \
    libapache2-mod-security2

# Enable required Apache modules
RUN a2enmod proxy proxy_fcgi rewrite headers security2 env setenvif dir mime

# Enable the hardening config
RUN a2enconf security

EXPOSE 80

# Start Apache in the foreground
CMD ["apachectl", "-D", "FOREGROUND"]
