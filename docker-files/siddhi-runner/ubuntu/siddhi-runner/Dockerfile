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

# use siddhi-runner-base
ARG SIDDHI_RUNNER_BASE_IMAGE=siddhiio/siddhi-runner-base-ubuntu:latest
FROM ${SIDDHI_RUNNER_BASE_IMAGE}
MAINTAINER Siddhi IO Docker Maintainers "siddhi-dev@googlegroups.com"

ARG HOST_BUNDLES_DIR=./files/bundles
ARG HOST_JARS_DIR=./files/jars
ARG JARS=${RUNTIME_SERVER_HOME}/jars
ARG BUNDLES=${RUNTIME_SERVER_HOME}/bundles

# copy entrypoint bash script to user home
COPY --chown=siddhi_user:siddhi_io init.sh ${WORKING_DIRECTORY}/

# copy bundles & jars to the siddhi-runner distribution
COPY --chown=siddhi_user:siddhi_io ${HOST_BUNDLES_DIR}/ ${BUNDLES}
COPY --chown=siddhi_user:siddhi_io ${HOST_JARS_DIR}/ ${JARS}

# expose ports
EXPOSE 9090 9443 9712 9612 7711 7611 7070 7443

RUN bash ${RUNTIME_SERVER_HOME}/bin/install-jars.sh

STOPSIGNAL SIGINT

ENTRYPOINT ["/home/siddhi_user/init.sh", "--"]