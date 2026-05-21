FROM mcr.microsoft.com/dotnet/sdk:10.0

# Install essential dev tools + 7-Zip
RUN apt-get update && apt-get install -y \
    git \
    curl \
    wget \
    unzip \
    7zip \
    procps \
    openssh-client \
    apt-transport-https \
    && rm -rf /var/lib/apt/lists/*

# Install PowerShell 7 via Microsoft package feed
RUN wget -q "https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb" \
    && dpkg -i packages-microsoft-prod.deb \
    && rm packages-microsoft-prod.deb \
    && apt-get update && apt-get install -y powershell \
    && rm -rf /var/lib/apt/lists/*

# Set up a non-root user
ARG USERNAME=developer
ARG USER_UID=1001
ARG USER_GID=1001

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update && apt-get install -y sudo \
    && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
    && rm -rf /var/lib/apt/lists/*

USER $USERNAME
WORKDIR /home/$USERNAME
