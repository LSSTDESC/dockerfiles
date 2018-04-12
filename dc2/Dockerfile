FROM lsstsqre/centos:7-stack-lsst_distrib-w_2018_09
MAINTAINER Heather Kelly <heather@slac.stanford.edu>

ARG LSST_STACK_DIR=/opt/lsst/software/stack
ARG LSST_WORK_DIR=/opt/lsst/software
ARG EUPS_TAG=w_2018_09
ARG BRANCH=w.2018.04-35-g11f44ee
ARG LSST_USER=lsst
ARG LSST_GROUP=lsst

WORKDIR $LSST_STACK_DIR

RUN echo "Environment: \n" && env | sort

RUN echo "Executing: eups distrib install $EUPS_PRODUCT $EUPS_TAG" && \
    source scl_source enable devtoolset-6 && \
    gcc --version && \
    echo -e "source scl_source enable devtoolset-6\n$(cat loadLSST.bash)" > loadLSST.bash && \
    echo -e "hooks.config.Eups.globalTags += [\"dc2\"]\n$(cat stack/current/site/startup.py)" > stack/current/site/startup.py && \
    /bin/bash -c 'source $LSST_STACK_DIR/loadLSST.bash; \
                  cd $LSST_STACK_DIR; \
                  setup lsst_distrib; \
                  git clone https://github.com/LSSTDESC/obs_lsstSim.git; \
                  cd obs_lsstSim; \
                  eups declare -r . obs_lsstSim -t dc2;\
                  setup -j -r .;\
                  scons; \
                  scons install; \
                  scons declare;' 


