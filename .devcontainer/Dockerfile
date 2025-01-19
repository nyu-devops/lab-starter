# Create a Base image for the container (Python 3.11)
FROM python:3.11-slim

# Install essential tools and utilities for development
RUN apt-get update && \
    apt-get install -y sudo vim make git zip tree curl wget jq && \
    apt-get autoremove -y && \
    apt-get clean -y

# Define user configuration for the development environment
ARG USERNAME=devops
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create a non-root user with sudo privileges for secure development
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME -s /bin/bash \
    && usermod -aG sudo $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Set the working directory for the application
WORKDIR /app

# Copy the Python dependencies file and install required packages
COPY requirements.txt .
RUN python -m pip install --upgrade pip wheel && \
    pip install -r requirements.txt

# Expose the default application port for easy access
ENV PORT=8000
EXPOSE $PORT

# Configure terminal colors for a better shell experience in the container
ENV TERM=xterm-256color

# Switch to the non-root user for all subsequent operations
USER $USERNAME
