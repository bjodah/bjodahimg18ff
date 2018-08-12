FROM bjodah/bjodahimg18:v1.3
MAINTAINER Björn Dahlgren <bjodah@DELETEMEgmail.com>
RUN apt-get update && \
    apt-get --quiet --assume-yes install libsundials-dev && \    
    python3 -m pip uninstall -y sympy && \
    python3 -m pip install --upgrade pyodeint>=0.9.8,<0.10.0 pygslodeiv2>=0.8.4,<0.9.0 pycvodes>=0.10.8,0.11.0 pyodesys>=0.11.16,<0.12.0 sympy>=1.1.1,!=1.2 block_diag_ilu>=0.3.9,<0.4.0 chemreac>=0.7.10,<0.8.0 chempy>=0.6.8,<0.7.0 && \
    python3 -m pytest --pyargs chempy --slow --veryslow && \

RUN mkdir /tmp/syme && cd /tmp/syme && curl -Ls https://github.com/symengine/symengine/archive/929022facc2b6b9d98540e47f8e523dfa0664545.tar.gz | tar xz && \
    mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE:STRING="Release" -DWITH_BFD:BOOL=ON -DBUILD_SHARED_LIBS:BOOL=ON \
    -DWITH_LLVM:BOOL=ON -DBUILD_TESTS:BOOL=OFF -DBUILD_BENCHMARKS:BOOL=OFF ../symengine-929022facc2b6b9d98540e47f8e523dfa0664545 && \
    make install

RUN python3 -m pip install http://hera.physchem.kth.se/~kinetgine/branches/kinetgine-0.3.x/pykinetgine-0.3.1.post2%2bg4dbd830.tar.gz && \
    python3 -m pytest --pyargs pykinetgine
