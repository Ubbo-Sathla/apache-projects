ARG BASE_IMAGE

FROM ${BASE_IMAGE:-centos:7.9.2009} AS ranger_builder

ENV PYENV_HOME /opt/pyenv
ENV PYENV_ROOT /opt/python
ENV PYTHON_VERSION 3.6.15
ENV PATH $PYENV_HOME/bin:$PATH

# Install Python3
RUN  yum  install -y make gcc patch wget git bzip2 fontconfig zlib-devel bzip2-devel openssl-devel ncurses-devel \
     sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel && yum clean all

RUN git clone https://github.com/pyenv/pyenv.git $PYENV_HOME && pyenv install $PYTHON_VERSION && \
     git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv && \
     pyenv virtualenv $PYTHON_VERSION ranger

ENV PATH $PYENV_ROOT/versions/$PYTHON_VERSION/envs/ranger/bin:$PATH

WORKDIR /opt

# https://www.oracle.com/uk/java/technologies/javase/javase8u211-later-archive-downloads.html
ENV JAVA_HOME /opt/jdk1.8.0_311
ENV PATH $JAVA_HOME/bin:$PATH
RUN wget -q http://10.127.252.101/dav/java/jdk-8u311-linux-x64.tar.gz && \
    tar -zxf jdk-8u311-linux-x64.tar.gz && rm -rf jdk-8u311-linux-x64.tar.gz

# https://maven.apache.org/download.cgi
ENV MAVEN_HOME /opt/apache-maven-3.8.4
ENV PATH $MAVEN_HOME/bin:$PATH
RUN wget -q http://10.127.252.101/dav/apache/maven/apache-maven-3.8.4-bin.tar.gz && \
    tar -zxf apache-maven-3.8.4-bin.tar.gz && rm -rf apache-maven-3.8.4-bin.tar.gz && \
    sed -i 's#external:http#external:tcp#g' /opt/apache-maven-3.8.4/conf/settings.xml

FROM ranger_builder

WORKDIR /opt/ranger

# https://ranger.apache.org/download.html
RUN wget -q http://10.127.252.101/dav/apache/ranger/apache-ranger-2.2.0.tar.gz && \
    tar -zxf apache-ranger-2.2.0.tar.gz && rm -rf apache-ranger-2.2.0.tar.gz

