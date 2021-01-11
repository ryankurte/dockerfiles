FROM debian:latest

RUN apt-get update -y && \
    apt-get install -y python3 python3-distutils curl && \
    apt-get clean && \
    rm -rf /var/lib/apt

RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python3 get-pip.py

RUN pip install awscli

RUN pip install anybadge

