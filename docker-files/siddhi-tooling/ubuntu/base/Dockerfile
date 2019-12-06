# ------------------------------------------------------------------------
#
# Copyright 2019 WSO2, Inc. (http://wso2.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License
#
# ------------------------------------------------------------------------

# set base Docker image to AdoptOpenJDK Ubuntu Docker image
FROM adoptopenjdk/openjdk8:jdk8u192-b12-slim
MAINTAINER Siddhi IO Docker Maintainers "siddhi-dev@googlegroups.com"

# set user configurations
ARG USER=siddhi_user
ARG USER_ID=802
ARG USER_GROUP=siddhi_io
ARG USER_GROUP_ID=802
ARG USER_HOME=/home/${USER}
# set dependant files directory
ARG FILES=./files
ARG PACK=pack
# set siddhi-tooling configurations
ARG RUNTIME_SERVER=siddhi-tooling
ARG RUNTIME_SERVER_VERSION=5.1.2
ARG RUNTIME_SERVER_PACK=${RUNTIME_SERVER}-${RUNTIME_SERVER_VERSION}
ARG RUNTIME_SERVER_HOME=${USER_HOME}/${RUNTIME_SERVER}
ARG RUNTIME_TYPE
# set SIDDHI-IO EULA
ARG MOTD="\n\
Welcome to Siddhi Docker resources.\n\
------------------------------------ \n\
This Docker container comprises of a SIDDHI-IO product, running with its latest GA release \n\
which is under the Apache License, Version 2.0. \n\
Read more about Apache License, Version 2.0 here @ http://www.apache.org/licenses/LICENSE-2.0.\n"

# create the user and group
RUN \
    groupadd --system -g ${USER_GROUP_ID} ${USER_GROUP} \
    && useradd --system --create-home --home-dir ${USER_HOME} --no-log-init -g ${USER_GROUP_ID} -u ${USER_ID} ${USER}

# install required packages
RUN \
    apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        java-common \
        netcat \
        unzip \
        wget \
        bash \
        vim \
        curl \
    && echo '[ ! -z "${TERM}" -a -r /etc/motd ] && cat /etc/motd' >> /etc/bash.bashrc; echo "${MOTD}" > /etc/motd

# install ant
ENV ANT_VERSION 1.10.6
RUN cd && \
    wget -q http://www.us.apache.org/dist//ant/binaries/apache-ant-${ANT_VERSION}-bin.tar.gz && \
    tar -xzf apache-ant-${ANT_VERSION}-bin.tar.gz && \
    mv apache-ant-${ANT_VERSION} /opt/ant && \
    rm apache-ant-${ANT_VERSION}-bin.tar.gz
ENV ANT_HOME /opt/ant
ENV PATH ${PATH}:/opt/ant/bin

## install the Siddhi Distribution to user's home directory

COPY --chown=siddhi_user:siddhi_io ${FILES}/${PACK}/ ${USER_HOME}/
# download Siddhi Tooling Distribution
RUN if [ ! -e ${USER_HOME}/${RUNTIME_SERVER}*.zip ] ; then wget --no-check-certificate -O ${USER_HOME}/${RUNTIME_SERVER_PACK}.zip "https://github.com/siddhi-io/distribution/releases/download/v${RUNTIME_SERVER_VERSION}/${RUNTIME_SERVER_PACK}.zip" \
    ; else echo "Using Local image "; fi 
    
RUN unzip -d ${USER_HOME} ${USER_HOME}/${RUNTIME_SERVER}*.zip && rm -f ${USER_HOME}/${RUNTIME_SERVER}*.zip && for file in ${USER_HOME}/${RUNTIME_SERVER}*; do mv $file ${USER_HOME}/${RUNTIME_SERVER}; done \
    && chown ${USER}:${USER_GROUP} -R ${RUNTIME_SERVER_HOME}

# set the user and work directory
USER ${USER_ID}
WORKDIR ${USER_HOME}

# set environment variables
ENV RUNTIME_SERVER_HOME=${RUNTIME_SERVER_HOME} \
    WORKING_DIRECTORY=${USER_HOME}
