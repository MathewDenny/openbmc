FROM ubuntu:focal
RUN apt-get update 
RUN apt-get install -y apt-utils tzdata
RUN apt-get -y install gawk wget git-core \
    diffstat unzip texinfo gcc-multilib build-essential \
    chrpath socat cpio python python3 python3-pip \
    python3-pexpect xz-utils debianutils iputils-ping \
    libsdl1.2-dev xterm tar locales
RUN rm /bin/sh && ln -s bash /bin/sh
RUN locale-gen en_US.UTF-8 && update-locale LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV USER_NAME rchow 
ENV PROJECT openbmc
ARG host_uid=1001
ARG host_gid=1001
RUN groupadd -g $host_gid $USER_NAME && \
    useradd -g $host_gid -m -s /bin/bash -u $host_uid $USER_NAME
USER $USER_NAME

ENV BUILD_INPUT_DIR /home/$USER_NAME/input
ENV BUILD_OUTPUT_DIR /home/$USER_NAME/output
RUN mkdir -p $BUILD_INPUT_DIR $BUILD_OUTPUT_DIR

WORKDIR $BUILD_INPUT_DIR
RUN git clone https://github.com/openbmc/$PROJECT.git

WORKDIR $BUILD_OUTPUT_DIR
ENV TEMPLATECONF=$BUILD_INPUT_DIR/$PROJECT/meta-ibm/meta-romulus/conf
RUN ls $BUILD_INPUT_DIR/$PROJECT
#Command
CMD source $BUILD_INPUT_DIR/$PROJECT/openbmc-env build && bitbake obmc-phosphor-image
