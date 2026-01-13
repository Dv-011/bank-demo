FROM nginx:1.25-alpine

# Create non-root user
RUN addgroup -S webgrp && adduser -S webusr -G webgrp

# Fix permissions for nginx runtime dirs
RUN mkdir -p /var/cache/nginx /var/run \
  && chown -R webusr:webgrp /var/cache/nginx /var/run /usr/share/nginx/html \
  && touch /var/run/nginx.pid \
  && chown webusr:webgrp /var/run/nginx.pid

COPY index.html /usr/share/nginx/html/index.html

USER webusr
