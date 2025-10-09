FROM almalinux

RUN yum install -y \
    make \
    gcc \
    gcc-c++ \
    ncurses* \
    libncurses* \
    libpng* \
    kernel-devel && \
    yum clean all

CMD ["/bin/bash"]
