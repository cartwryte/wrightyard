# Use the official lightweight Apache image
FROM httpd:2.4-alpine

# --- Configuration ---

# Copy our custom server configuration file
COPY docker/apache/conf/httpd.conf /usr/local/apache2/conf/httpd.conf

# Create the directory for site-specific configurations
RUN mkdir -p /usr/local/apache2/conf/sites-available

# Copy our OpenCart-specific site configuration
COPY docker/apache/conf/opencart.conf /usr/local/apache2/conf/sites-available/opencart.conf

# --- Entrypoint ---

# Copy our custom entrypoint script that waits for the PHP service
COPY docker/apache/docker-apache-entrypoint /usr/local/bin/

# Make the entrypoint script executable
RUN chmod +x /usr/local/bin/docker-apache-entrypoint

# Set our script as the entrypoint for the container
ENTRYPOINT ["docker-apache-entrypoint"]

# The default command to run after our entrypoint finishes, inherited from the base image
CMD ["httpd-foreground"]
