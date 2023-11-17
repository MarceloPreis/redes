FROM internetsystemsconsortium/bind9:9.19

RUN apt update \
  && apt install -y \
  bind9-doc \
  dnsutils \
  geoip-bin \
  mariadb-server \
  net-tools

# DNS config
COPY dns/named.conf.options /etc/bind/
COPY dns/named.conf.local /etc/bind/
COPY dns/db.angelita.corp /etc/bind/zones/

# NGNIX config
COPY web/nginx.conf /etc/nginx/nginx.conf
COPY web/default.conf /etc/nginx/conf.d/default.conf
COPY web/intranet.conf /etc/nginx/conf.d/intranet.conf
RUN mkdir -p /var/www && echo "Hello, World!" > /var/www/index.html

# Expose Ports
EXPOSE 53/tcp
EXPOSE 53/udp
EXPOSE 953/tcp

# Start the Name Service
CMD ["/usr/sbin/named", "-g", "-c", "/etc/bind/named.conf", "-u", "bind"]
