FROM debian:jessie

MAINTAINER kdxu <kyoko.kadowaki@gmail.com>

# Set environment.
ENV \
  DEBIAN_FRONTEND=noninteractive \
  TERM=xterm-color

# Install packages.
RUN apt-get update && apt-get -y install \
  build-essential \
  wget

# Install packages.
RUN \
  wget -qO - https://openresty.org/package/pubkey.gpg | apt-key add - && \
  apt-get -y install software-properties-common && \
  add-apt-repository -y "deb http://openresty.org/package/debian $(lsb_release -sc) openresty" && \
  apt-get update && \
  apt-get -y install --no-install-recommends openresty && \
  ln -s /usr/local/openresty/nginx/sbin/nginx /usr/local/bin/nginx && \
  ldconfig

# Set the working directory.
WORKDIR /home/openresty

# Add files to the container.
ADD . /home/openresty

# Expose volumes.
VOLUME ["/etc/nginx"]

# Set the entrypoint script.
ENTRYPOINT ["./entrypoint"]

# Define the default command.
CMD ["nginx", "-c", "/etc/nginx/nginx.conf"]
