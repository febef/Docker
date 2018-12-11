# Dockerizing MongoDB: Dockerfile for building MongoDB images
# Based on ubuntu:16.04, installs MongoDB following the instructions from:
# http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

FROM debian:stretch
MAINTAINER febef - Facundo Beltramo (fexbef@gmail.com)

# Installation:
# Import MongoDB public GPG key AND create a MongoDB list file

# Update apt-get sources AND install MongoDB
RUN apt-get update && apt-get install -y mongodb ; \
    echo "#!/bin/bash" > "/usr/entrypoint.sh" ; \
    echo "service mongodb start" >> "/usr/entrypoint.sh" ; \
    chmod +x "/usr/entrypoint.sh"; \
# Create the MongoDB data directory
    mkdir -p /data/db ;

# Expose port #27017 from the container to the host
EXPOSE 27017

# Set /usr/bin/mongod as the dockerized entry-point application
ENTRYPOINT ["/usr/entrypoint.sh"]
