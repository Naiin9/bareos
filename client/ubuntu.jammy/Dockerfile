FROM ubuntu:jammy

LABEL maintainer="Naiin9 <naiin9@outlook.com>"

RUN /bin/sh -c set -ex; \
        apt-get update -qq; \
        apt-get install -qq -y wget gnupg tzdata; \
        wget -qO- https://download.bareos.org/current/xUbuntu_22.04/add_bareos_repositories.sh | bash; \
        apt-get update -qq; \
        apt-get install -qq -y bareos-client; \
        apt-get clean; \
        rm -rf /var/lib/apt/lists/*;

# Set default timezone to Asia/Bangkok
ENV TZ=Asia/Bangkok
RUN ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

EXPOSE 9102/tcp

CMD ["/usr/sbin/bareos-fd", "-f"]
