# CWS Parent Portal Docker

The CWS Parent Portal Docker project provides Docker configuration to build and deploy the CWS Parent Portal
application.

The root of the project contains configuration for Docker Compose, a tool for defining and running multi-container
Docker applications.

The jenkins directory contains the Dockerfile and related artifacts required to create the Jenkins Docker container
used to implement the continuous delivery pipeline for the CWS Parent Portal. The jenkins configuration has a separate
[README][jenkinsreadme] file and is not covered in this document.

## Configuration

## Installation

### Prerequisites

1. Docker Compose 1.7+

### Using Docker Compose


[jenkinsreadme]: jenkins/README.md