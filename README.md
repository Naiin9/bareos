# Naiin9/bareos - Compact Docker Images for Bareos Components

[![Docker Pulls - File Daemon](https://img.shields.io/docker/pulls/naiin9/bareos-filedaemon.svg)](https://hub.docker.com/r/naiin9/bareos-filedaemon/)

---

**Overview**

This repository contains Dockerfiles and resources to build Docker images for components of the [Bareos backup, archiving, and restoration system](https://www.bareos.org/).

The primary objective of this repository is to provide **minimal, lightweight, and efficient** Docker images for each Bareos component. We aim to include only the necessary Bareos binaries and dependencies to reduce image size and improve resource usage.

Currently, the focus is on providing a compact image for the **Bareos File Daemon (FD)**. This repository also includes build contexts for the Bareos Director and Storage Daemon, built with the same philosophy of keeping images as small as possible.

**What's Inside**

This repository includes Docker build contexts for:

* `./bareos-filedaemon`: Contains the Dockerfile and assets for the **Bareos File Daemon (FD)** image (`naiin9/bareos-filedaemon`).

**Building the Images**

Clone the repository and navigate to the root directory. Then, build each image individually:

```bash
git clone https://github.com/Naiin9/bareos.git
cd bareos

# Build Bareos File Daemon image
docker build -t <tag for bareos-filedaemon> ./bareos-filedaemon
