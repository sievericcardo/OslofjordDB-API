# syntax=docker/dockerfile:1.3-labs

# To build the container:
#     docker build -f DockerfileFuseki -t fuseki .
# To run smol in the current directory:
#     docker run -it --rm -v "$PWD":/root/smol -p 3030:3030 fuseki

# Use a base image, for example, Ubuntu
FROM ubuntu:latest

RUN <<EOF
    apt-get -y update
    DEBIAN_FRONTEND=noninteractive apt-get -y install openjdk-17-jdk-headless python3 python3-pip liblapack3 wget
    rm -rf /var/lib/apt/lists/*
EOF
COPY . /fuseki
COPY /docker_fuseki_config.ttl /fuseki

# Set the working directory
WORKDIR /fuseki

# Download and copy the tar.gz file into the container
ADD https://dlcdn.apache.org/jena/binaries/apache-jena-fuseki-5.0.0.tar.gz /fuseki

# Extract the tar.gz file
RUN tar -xvzf apache-jena-fuseki-5.0.0.tar.gz

# Execute the command
CMD /fuseki/apache-jena-fuseki-5.0.0/fuseki-server --update --config docker_fuseki_config.ttl

# Expose port 3030
EXPOSE 3030