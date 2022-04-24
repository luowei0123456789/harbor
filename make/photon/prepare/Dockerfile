ARG harbor_base_image_version
FROM feiteng.harbor.ctyun.cn:5000/feitengky10/caas/photon:3.0

RUN rm -rf /etc/yum.repos.d/*
COPY ./make/photon/packages/config/harbor.repo /etc/yum.repos.d/harbor.repo

RUN tdnf install -y python3 \
    && tdnf install -y python3-pip python3-PyYAML python3-jinja2

#RUN pip3 install setuptools && pip3 install pipenv==2021.5.29
WORKDIR /usr/src/app
COPY make/photon/packages/pip/ /usr/src/app/

RUN cd /usr/src/app && \
	pip3 install ./setuptools-36.2.1-py2.py3-none-any.whl && \
	pip3 install ./certifi-2019.11.28-py2.py3-none-any.whl && \
	pip3 install ./six-1.9.0-py2.py3-none-any.whl && \
	pip3 install ./zipp-0.5.0-py2.py3-none-any.whl && \
	pip3 install ./filelock-3.1.0-py2.py3-none-any.whl && \
	pip3 install ./distlib-0.3.1-py2.py3-none-any.whl && \
	pip3 install ./importlib_metadata-0.12-py2.py3-none-any.whl && \
	pip3 install ./appdirs-1.4.3-py2.py3-none-any.whl && \
	pip3 install ./virtualenv_clone-0.3.0-py2.py3-none-any.whl && \
	pip3 install ./virtualenv-20.4.5-py2.py3-none-any.whl && \
	pip3 install ./pipenv-2018.11.26-py3-none-any.whl && \
	pip3 install ./MarkupSafe-1.1.1.tar.gz  && \
	pip3 install ./pyparsing-2.4.7-py2.py3-none-any.whl && \
	pip3 install ./packaging-20.9-py2.py3-none-any.whl && \
	pip3 install ./click-7.1.2-py2.py3-none-any.whl && \
	pip3 install ./Jinja2-2.11.3-py2.py3-none-any.whl

ENV LANG en_US.UTF-8

WORKDIR /usr/src/app

RUN mkdir -p /harbor_make

COPY make/photon/prepare /usr/src/app
RUN set -ex && pipenv install --deploy --system

ENTRYPOINT [ "python3", "main.py" ]

VOLUME ["/harbor_make"]