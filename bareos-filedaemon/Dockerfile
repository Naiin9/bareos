# docker buildx build -t bareos-filedaemon:latest .
# Stange #1 - Build
FROM ubuntu:latest AS builder
ARG BUILD_DIR=/builder

RUN /bin/sh -c set -ex; \
        apt-get update -qq; \
        apt-get install -qq -y wget gnupg tzdata python3; \
        wget -qO- https://download.bareos.org/current/xUbuntu_22.04/add_bareos_repositories.sh | bash; \
        apt-get update -qq; \
        apt-get install -qq -y bareos-filedaemon; \
        apt-get clean; \
        rm -rf /var/lib/apt/lists/*;


# Set default timezone to Asia/Bangkok
ENV TZ=Asia/Bangkok
RUN ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Create root fs for final image
RUN mkdir ${BUILD_DIR}

# Solve COPY to preserved symlink
RUN tar -czf zoneinfo.tar.gz -C / usr/share/zoneinfo etc/localtime etc/timezone
RUN tar -xzvf zoneinfo.tar.gz  -C ${BUILD_DIR}

# 
COPY depcp.py /
RUN chmod +x depcp.py

RUN /depcp.py /usr/sbin/bareos-fd ${BUILD_DIR} #copy bareos-fd and dependencies
RUN mkdir -p ${BUILD_DIR}/var/lib/bareos #patch missing dir
RUN mkdir -p ${BUILD_DIR}/etc/bareos #patch missing dir; bareos-fd config
COPY bareos-fd.config/ ${BUILD_DIR}/etc/bareos


# Stage #2 - Create Final Image
FROM alpine:latest
ARG BUILD_DIR=/builder

LABEL maintainer="Naiin9 <naiin9@outlook.com>"

COPY --from=builder ${BUILD_DIR}/ /
EXPOSE 9102/tcp

CMD ["/usr/sbin/bareos-fd", "-f"]
