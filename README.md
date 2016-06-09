# CWS Parent Portal Docker

The CWS Parent Portal Docker project provides Docker configuration to build and deploy the CWS Parent Portal
application.

The root of the project contains configuration for Docker Compose, a tool for defining and running multi-container
Docker applications. This document details configuration and usage of Docker Compose to run the application.

The jenkins directory contains the Dockerfile and related artifacts required to create the Jenkins Docker container
used to implement the continuous delivery pipeline for the CWS Parent Portal. The jenkins configuration has a separate
[README][jenkinsreadme] file and is not covered in this document.

## Configuration

The CWS Parent Portal application requires configuration of the env.js file prior to deployment. Edit the ui/env.js
file in this repository and replace the ```baseurl``` variable with the location where the UI code, running in a
browser, can contact the CWS Parent Portal API running instance.

Additionally, the UI, API and Postgres containers take standard Docker configuration options for volumes, ports and
environment variables. Each container describes specific configuration options and the default configuration provides
a working deployment out of the box.

## Installation

This Docker project should be considered a framework and example deployment configuration. As such, it is not installed
so much as it is cloned using Git and customized to suit the deployment environment.

If the operator will be running from local development containers (see below), then the UI and API projects will need to
be checked out:

    % git clone https://github.com/taborda-cws-prototype/cws-parent-portal-api.git
    % git clone https://github.com/taborda-cws-prototype/cws-parent-portal-ui.git

### Prerequisites

1. Docker Compose 1.7
1. Git 2.8

### Using Docker Compose

The docker-compose.yml file is suitable for local development. The docker-compose file builds local images from
source, reflecting the local system's current state. To run from the local images, execute the builds for the UI and
API projects (reference project README files) and then run the system with Docker Compose.

    % docker-compose up

[dockercompose]: https://docs.docker.com/compose/
[jenkinsreadme]: jenkins/README.md
