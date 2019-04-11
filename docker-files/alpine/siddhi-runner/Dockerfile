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
FROM siddhi-runner-base:1.0.0-m3-alpine
MAINTAINER Siddhi IO Docker Maintainers "siddhi-dev@googlegroups.com"

ARG BUNDLE_JAR_DIR=./files/lib
ARG LIB=${RUNTIME_SERVER_HOME}/lib
# copy entrypoint bash script to user home
COPY --chown=siddhi_user:siddhi_io init.sh ${WORKING_DIRECTORY}/

# copy bundle jars to the siddhi-runner pack
COPY --chown=siddhi_user:siddhi_io ${BUNDLE_JAR_DIR}/ ${LIB}

# expose ports
EXPOSE 9090 9443 9712 9612 7711 7611 7070 7443

ENTRYPOINT ["/home/siddhi_user/init.sh"]
