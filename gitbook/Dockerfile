FROM node:current-buster-slim

# Install deps
RUN apt-get update -y && \
    apt-get install -y \
    git calibre \
    python3 python3-pip

# Install gitbook
RUN npm install -g gitbook-cli && \
    gitbook fetch

CMD gitbook pdf

