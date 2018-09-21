FROM lsstsqre/centos:7-stack-lsst_distrib-w_2018_30
MAINTAINER Heather Kelly <heather@slac.stanford.edu>

ARG LSST_STACK_DIR=/opt/lsst/software/stack
ARG LSST_USER=lsst
ARG LSST_GROUP=lsst

WORKDIR $LSST_STACK_DIR

RUN echo "Environment: \n" && env | sort

RUN echo "Installing ipykernel" && \
    /bin/bash -c 'source $LSST_STACK_DIR/loadLSST.bash; \
                  conda install -y ipykernel' 


