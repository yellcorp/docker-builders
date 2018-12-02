FROM node:8.9

LABEL maintainer="Jim Boswell <jimb@yellcorp.org>"
LABEL version=0.0.1
LABEL description="Build image based off official Node 8.x, adding pip for Python"

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
      python-dev \
      python-pip \
 && rm -rf /var/lib/apt/lists/*
