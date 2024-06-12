# Repo: https://github.com/QuokkaStake/cosmos-validators-exporter
# Use the official Ubuntu image as the base image
FROM ubuntu:latest

# Set the application version as an environment variable
ENV VERSION=5.8.0

# Install required packages
RUN apt-get update && apt-get install -y wget

# Download and install the application
RUN wget https://github.com/QuokkaStake/cosmos-validators-exporter/releases/download/v${VERSION}/cosmos-validators-exporter_${VERSION}_linux_amd64.deb \
    && apt-get install -y ./cosmos-validators-exporter_${VERSION}_linux_amd64.deb \
    && rm cosmos-validators-exporter_${VERSION}_linux_amd64.deb

# Create a directory for the config file
RUN mkdir /config

# Set the entrypoint command
ENTRYPOINT ["cosmos-validators-exporter", "--config", "/config/config.toml"]

# Expose any ports the service uses (optional, adjust as necessary)
EXPOSE 9560