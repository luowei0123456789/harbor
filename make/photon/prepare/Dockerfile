ARG harbor_base_image_version
FROM photon:3.0

RUN tdnf install -y python3 \
    && tdnf install -y python3-pip python3-PyYAML python3-jinja2
RUN pip3 install setuptools && pip3 install pipenv==2021.5.29
ENV LANG en_US.UTF-8

WORKDIR /usr/src/app

RUN mkdir -p /harbor_make

COPY make/photon/prepare /usr/src/app
RUN set -ex && pipenv install --deploy --system

ENTRYPOINT [ "python3", "main.py" ]

VOLUME ["/harbor_make"]