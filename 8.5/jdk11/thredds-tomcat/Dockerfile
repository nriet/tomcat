###
# Dockerfile for Unidata Tomcat.
###
FROM tomcat:8.5-jdk11

MAINTAINER axiu

# netcdf envs
ENV LD_LIBRARY_PATH /usr/local/lib:${LD_LIBRARY_PATH}
ENV HDF5_VERSION 1.12.2
ENV ZLIB_VERSION 1.2.9
ENV NETCDF_VERSION 4.9.2
ENV ZDIR /usr/local
ENV H5DIR /usr/local
ENV PDIR /usr
ENV HDF5_VER hdf5-${HDF5_VERSION}
ENV HDF5_FILE ${HDF5_VER}.tar.gz

# Install necessary packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends  \
        gosu \
        zip \
        unzip \
        vim build-essential m4 \
        libpthread-stubs0-dev libcurl4-openssl-dev && \
    # Cleanup
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    # Eliminate default web applications
    rm -rf ${CATALINA_HOME}/webapps/* && \
    rm -rf ${CATALINA_HOME}/webapps.dist && \
    # Obscuring server info
    cd ${CATALINA_HOME}/lib && \
    mkdir -p org/apache/catalina/util/ && \
    unzip -j catalina.jar org/apache/catalina/util/ServerInfo.properties \
        -d org/apache/catalina/util/ && \
    sed -i 's/server.info=.*/server.info=Apache Tomcat/g' \
        org/apache/catalina/util/ServerInfo.properties && \
    zip -ur catalina.jar \
        org/apache/catalina/util/ServerInfo.properties && \
    rm -rf org && cd ${CATALINA_HOME} && \
    # Setting restrictive umask container-wide
    echo "session optional pam_umask.so" >> /etc/pam.d/common-session && \
    sed -i 's/UMASK.*022/UMASK           007/g' /etc/login.defs && \
    # zlib
    curl https://zlib.net/fossils/zlib-${ZLIB_VERSION}.tar.gz | tar xz && \
    cd zlib-${ZLIB_VERSION} && \
    ./configure --prefix=/usr/local && \
    make && make install && \
    cd .. && rm -rf zlib-${ZLIB_VERSION} && \
    # hdf
    curl https://support.hdfgroup.org/ftp/HDF5/releases/${HDF5_VER%.*}/${HDF5_VER}/src/${HDF5_FILE} | tar xz && \
    cd hdf5-${HDF5_VERSION} && \
    ./configure --with-zlib=${ZDIR} --prefix=${H5DIR} --enable-threadsafe --with-pthread=${PDIR} --enable-unsupported --prefix=/usr/local && \
    make && make check && make install && make check-install && ldconfig && \
    cd .. && rm -rf hdf5-${HDF5_VERSION} && \
    # netcdf
    export CPPFLAGS=-I/usr/local/include \
    LDFLAGS=-L/usr/local/lib && \
    curl https://downloads.unidata.ucar.edu/netcdf-c/${NETCDF_VERSION}/netcdf-c-${NETCDF_VERSION}.tar.gz | tar xz && \
    cd netcdf-c-${NETCDF_VERSION} && \
    ./configure --disable-dap-remote-tests --disable-libxml2 --prefix=/usr/local && \
    make check && make install && ldconfig && \
    cd .. && rm -rf netcdf-c-${NETCDF_VERSION} 

# Security enhanced web.xml
COPY web.xml ${CATALINA_HOME}/conf/

# Security enhanced server.xml
COPY server.xml ${CATALINA_HOME}/conf/

# Tomcat start script
COPY start-tomcat.sh ${CATALINA_HOME}/bin
COPY entrypoint.sh /

# Start container
ENTRYPOINT ["/entrypoint.sh"]
CMD ["start-tomcat.sh"]
