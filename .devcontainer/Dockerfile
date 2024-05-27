FROM mcr.microsoft.com/devcontainers/base:ubuntu-20.04

ENV ACCEPT_EULA=Y
ENV DEBIAN_FRONTEND=noninteractive

# Add MSSQL source drivers
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
  && echo "deb [arch=amd64] https://packages.microsoft.com/ubuntu/20.04/prod focal main" | tee /etc/apt/sources.list.d/mssql-release.list

# Add Gum to source lists
RUN mkdir -p /etc/apt/keyrings \
  && curl -fsSL https://repo.charm.sh/apt/gpg.key | gpg --dearmor -o /etc/apt/keyrings/charm.gpg \
  && echo "deb [signed-by=/etc/apt/keyrings/charm.gpg] https://repo.charm.sh/apt/ * *" | tee /etc/apt/sources.list.d/charm.list

# Update system packages
RUN apt-get update -y && apt-get upgrade -y && apt-get autoremove -y

# install chrome
RUN curl -sSL https://dl.google.com/linux/direct/google-chrome-stable_current_$(dpkg --print-architecture).deb -o /tmp/chrome.deb \
    && apt-get -y install /tmp/chrome.deb

# install lib dependencies
RUN apt-get install -y --no-install-recommends build-essential postgresql postgresql-contrib \
  # Cypress
  libgtk2.0-0 libgtk-3-0 libgbm-dev libnotify-dev libnss3 libxss1 libasound2 libxtst6 xauth xvfb \
  # utils
  gum msodbcsql17 libpq-dev dnsutils inetutils-ping telnet openvpn cpu-checker
