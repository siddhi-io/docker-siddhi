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

# use siddhi-tooling-base
FROM siddhiio/siddhi-tooling-base:5.1.0-m1
MAINTAINER Siddhi IO Docker Maintainers "siddhi-dev@googlegroups.com"

ARG BUNDLE_JAR_DIR=./files/lib
ARG LIB=${RUNTIME_SERVER_HOME}/lib

# copy entrypoint bash script to user home
COPY --chown=siddhi_user:siddhi_io init.sh ${WORKING_DIRECTORY}/

# copy bundle jars to the siddhi-tooling pack
COPY --chown=siddhi_user:siddhi_io ${BUNDLE_JAR_DIR}/ ${LIB}

# expose ports
EXPOSE 9743 9390 7370 7714 7614 9614 9714

STOPSIGNAL SIGINT

ENTRYPOINT ["/home/siddhi_user/init.sh", "--"]