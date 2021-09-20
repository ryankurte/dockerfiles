FROM espressif/idf:latest
LABEL maintainer = "Ryan Kurte <ryankurte@gmail.com>
LABEL description = "(temporary) ESP IDF with patched espcoredump.py for sentry.io upload \
see https://github.com/espressif/esp-idf/pull/7540 for detail"

# Install new deps
RUN . /opt/esp/idf/export.sh && pip3 install uuid construct

# Copy updated espcoredump tool
COPY espcoredump.py /opt/esp/idf/components/espcoredump/espcoredump.py
