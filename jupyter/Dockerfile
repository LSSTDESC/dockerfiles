FROM lsstsqre/centos:7-stack-lsst_distrib-w_2018_30
MAINTAINER Heather Kelly <heather@slac.stanford.edu>

ARG LSST_STACK_DIR=/opt/lsst/software/stack
ARG LSST_USER=lsst
ARG LSST_GROUP=lsst

WORKDIR $LSST_STACK_DIR

RUN echo "Environment: \n" && env | sort

USER root
RUN yum install -y libffi-devel
USER lsst

RUN echo "Installing ipykernel" && \
    /bin/bash -c 'source $LSST_STACK_DIR/loadLSST.bash; \
                  conda install -y ipykernel jupyter_console; \
                  pip install camb; \
                  pip install fast3tree; \
                  pip install fitsio; \
                  pip install healpy; \
                  pip install https://bitbucket.org/yymao/helpers/get/master.zip; \
                  conda install -y markupsafe nose; \
                  pip install parsl==0.6.1; \
                  export PYMSSQL_BUILD_WITH_BUNDLED_FREEETDS=1; \
                  pip install pymssql; \
                  pip install tables; \
                  pip install TreeCorr==3.3.7; \
                  pip install https://github.com/LSSTDESC/descqa/archive/v2.0.0-0.6.0.tar.gz; \
                  pip install https://github.com/LSSTDESC/gcr-catalogs/archive/v0.9.0.tar.gz; \
                  pip install corner; \
                  pip install https://github.com/yymao/FoFCatalogMatching/archive/v0.1.0.tar.gz; \
                  pip install git+https://github.com/msimet/Stile; \
                  pip install scikit-image; \
                  conda install -y cmake swig; \
                  setup fftw; \
                  setup gsl; \
                  pip install pyccl==0.3.4'


RUN echo "Installing obs_lsstCam" && \
    /bin/bash -c 'source $LSST_STACK_DIR/loadLSST.bash; \
                 setup lsst_distrib; \
                 git clone https://github.com/lsst/obs_lsstCam.git; \
                 cd obs_lsstCam; \
                 git checkout dc2/run1.2i; \
                 setup -r . -j; \
                 scons; \
                 cd ..'
