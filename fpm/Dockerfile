FROM ubuntu:latest

# Install necessary dependencies for FPM
RUN apt-get update && apt-get install -y \
    curl \
    gnupg \
    ruby \
    ruby-dev \
    build-essential \
    rpm

# Install FPM gem
RUN gem install --no-document fpm

# Set bash as the default command
CMD ["bash"]
