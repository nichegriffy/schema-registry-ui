FROM alpine
MAINTAINER Marios Andreopoulos <marios@landoop.com>

WORKDIR /
# Add needed tools
RUN apk add --no-cache ca-certificates wget \
    && echo "progress = dot:giga" | tee /etc/wgetrc

# Add and Setup Caddy webserver
RUN wget "https://github.com/mholt/caddy/releases/download/v0.9.5/caddy_linux_amd64.tar.gz" -O /caddy.tgz \
    && mkdir caddy \
    && tar xzf caddy.tgz -C /caddy \
    && mv /caddy/caddy_linux_amd64 /caddy/caddy \
    && rm -f /caddy.tgz

# Add and Setup Schema-Registry-Ui
RUN wget "https://github.com/Landoop/schema-registry-ui/releases/download/v.0.9.1/schema-registry-ui-0.9.1.tar.gz" \
         -O /schema-registry-ui.tar.gz \
    && mkdir /schema-registry-ui \
    && tar xzf /schema-registry-ui.tar.gz -C /schema-registry-ui \
    && rm -f /schema-registry-ui.tar.gz

# Add configuration and runtime files
ADD Caddyfile /caddy/Caddyfile.template
ADD run.sh /
RUN chmod +x /run.sh

EXPOSE 7000
ENTRYPOINT ["/run.sh"]
