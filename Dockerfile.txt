FROM ubuntu:latest

# run dpkg without interaction
ENV DEBIAN_FRONTEND=noninteractive

# update available packages
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
    libguestfs-tools
    #qemu-utils \
    #linux-image-generic

# Set a default working dir
RUN mkdir /build
WORKDIR /build

# run as root
ENV USER root

# Set entrypoint
COPY entrypoint.sh /usr/local/bin/
ENTRYPOINT ["/bin/sh", "/usr/local/bin/entrypoint.sh"]