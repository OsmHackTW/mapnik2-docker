FROM osmtw/ubuntu:trusty
MAINTAINER Rex Tsai <rex.cc.tsai@gmail.com>

ENV MAPNIK_VERSION=2.2.0+ds1-6build2 \
    PYTHON_MAPNIK_VERSION=2.2.0+ds1-6build2

# Verify that Mapnik has been installed correctly
RUN apt-get install -y \
            libmapnik2.2=${MAPNIK_VERSION} \
            libmapnik-dev=${MAPNIK_VERSION} \
            mapnik-utils=${MAPNIK_VERSION} \
            python-mapnik2=${PYTHON_MAPNIK_VERSION} \
 && python -c 'import mapnik'

# Install Cascadenik
RUN apt-get install -y git python-cssutils python-imaging \
 && git clone --depth 1 https://github.com/mapnik/Cascadenik.git \
 && cd Cascadenik \
 && python setup.py install \
 && cd - \
 && rm -r Cascadenik

# Install nik2img
RUN apt-get install -y python-setuptools \
 && easy_install -U nik2img


# Clean up APT when done
RUN apt-get autoremove -y --purge build-essential \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /build
