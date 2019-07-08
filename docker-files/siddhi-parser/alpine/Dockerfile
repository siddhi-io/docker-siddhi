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

# set base Docker image to AdoptOpenJDK Alpine Docker image
FROM adoptopenjdk/openjdk8:jdk8u192-b12-alpine
MAINTAINER Siddhi IO Docker Maintainers "siddhi-dev@googlegroups.com"

# set user configurations
ARG USER=siddhi_user
ARG USER_ID=802
ARG USER_GROUP=siddhi_io
ARG USER_GROUP_ID=802
ARG USER_HOME=/home/${USER}
# set dependant files directory
ARG FILES=./files
# set siddhi runner configurations
ARG SIDDHI_PARSER_SERVICE_PACKAGENAME=siddhi.parser
ARG SIDDHI_PARSER_VERSION=0.2.0-m1
ARG SIDDHI_PARSER_SERVICE_JAR=${SIDDHI_PARSER_SERVICE_PACKAGENAME}-${SIDDHI_PARSER_VERSION}.jar
# set SIDDHI-IO EULA
ARG MOTD="\n\
Welcome to Siddhi Docker resources.\n\
------------------------------------ \n\
This Docker container comprises of a SIDDHI-IO product, running with its latest GA release \n\
which is under the Apache License, Version 2.0. \n\
Read more about Apache License, Version 2.0 here @ http://www.apache.org/licenses/LICENSE-2.0.\n"

# install required packages
RUN  apk add --update --no-cache netcat-openbsd && \
     rm -rf /var/cache/apk/*

# create a user group and a user
RUN  addgroup -g ${USER_GROUP_ID} ${USER_GROUP}; \
     adduser -u ${USER_ID} -D -g '' -h ${USER_HOME} -G ${USER_GROUP} ${USER} ;

# set the user and work directory
USER ${USER_ID}
WORKDIR ${USER_HOME}

# set environment variables
ENV WORKING_DIRECTORY=${USER_HOME}

# copy Siddhi Parser Service JAR and dependencies
COPY --chown=siddhi_user:siddhi_io ./files ${WORKING_DIRECTORY}/

CMD ["java", "-cp", "siddhi.parser-0.2.0-m1.jar:lib/*", "io.siddhi.operator.parser.services.Application"]
