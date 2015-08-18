FROM python:2.7

MAINTAINER "Victor Fernandez de Alba" <sneridagh@gmail.com>

ENV PYTHON python
ENV CONFIG builds/docker.genwebupc.cfg
ENV SETUPTOOLS 7.0
ENV ZCBUILDOUT 2.2.1
ENV PLONE_HOME /var/plone


RUN rm -rf $PLONE_HOME/* \
    && git clone https://github.com/UPCnet/genweb.buildout.git $PLONE_HOME/genweb.devel \
    && cd $PLONE_HOME/genweb.devel

COPY start.sh           /usr/bin/start
COPY install.sh         $PLONE_HOME/genweb.devel/

WORKDIR $PLONE_HOME/genweb.devel
RUN ./install.sh
VOLUME $PLONE_HOME/src/

CMD ["start"]
