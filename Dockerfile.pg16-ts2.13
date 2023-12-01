FROM timescale/timescaledb-ha:pg16-ts2.13

# Switch to root user for apt operations
USER root

# Install OpenSSL and sudo
RUN apt-get update && apt-get install -y openssl sudo

# Allow the postgres user to execute certain commands as root without a password
RUN echo "postgres ALL=(root) NOPASSWD: /usr/bin/mkdir, /bin/chown" > /etc/sudoers.d/postgres

# Add entrypoint wrapper
COPY wrapper.sh /usr/local/bin/wrapper.sh

# Add init script
COPY init-ssl.sh /docker-entrypoint-initdb.d/

# Set permissions
RUN chmod +x /usr/local/bin/wrapper.sh
RUN chmod +x /docker-entrypoint-initdb.d/init-ssl.sh

# Switch back to the postgres
USER postgres

# Override the ENTRYPOINT with a wrapper script
ENTRYPOINT ["wrapper.sh"]

# Start postgres listening on port 5432
CMD ["postgres", "--port=5432"]