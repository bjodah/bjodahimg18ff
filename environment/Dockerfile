FROM bjodah/bjodahimg18:v1.3
MAINTAINER Björn Dahlgren <bjodah@DELETEMEgmail.com>
RUN apt-get update && \
    apt-get --quiet --assume-yes install libsundials-dev && \    
    python3 -m pip uninstall -y sympy

RUN mkdir /tmp/syme && cd /tmp/syme && curl -Ls https://github.com/symengine/symengine/archive/929022facc2b6b9d98540e47f8e523dfa0664545.tar.gz | tar xz && \
    mkdir build && cd build && cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE:STRING="Release" -DWITH_BFD:BOOL=ON -DBUILD_SHARED_LIBS:BOOL=ON \
        -DWITH_LLVM:BOOL=ON -DBUILD_TESTS:BOOL=OFF -DBUILD_BENCHMARKS:BOOL=OFF ../symengine-929022facc2b6b9d98540e47f8e523dfa0664545 && \
    make install && cd .. && rm -r build symengine-*/ && \
    curl -Ls https://github.com/symengine/symengine.py/archive/7b158d20013c91d229fd574ca68e6c47e3568b37.tar.gz | tar xz && \
    cd symengine.py-7b158d20013c91d229fd574ca68e6c47e3568b37 && python3 setup.py install && cd .. && rm -r symengine.py-* && \
    python3 -c 'import symengine; assert symengine.test()'

RUN python3 -m pip install --upgrade "pyodeint>=0.9.8,<0.10.0" "pygslodeiv2>=0.8.4,<0.9.0" "pycvodes>=0.10.10,<0.11.0" "pycodeexport>=0.1.2,<0.2.0" "pycompilation>=0.4.3,<0.5.0" notebook "matplotlib>=2.2.3,<3.0.0" && \
    python3 -m pip install --upgrade "pyodesys>=0.11.16,<0.12.0" "sympy>=1.1.1,!=1.2" "block_diag_ilu>=0.3.9,<0.4.0" "finitediff>=0.6.2" && \
    python3 -m pip install --upgrade "chempy>=0.6.9,<0.7.0" && \
    python3 -m pip install --upgrade "chemreac>=0.7.10,<0.8.0" && \
    python3 -m pytest --pyargs chempy

RUN python3 -m pip install http://hera.physchem.kth.se/~kinetgine/releases/pykinetgine-0.3.2.tar.gz && \
    python3 -m pytest --pyargs pykinetgine && \
    python3 -m pip install http://hera.physchem.kth.se/~aq_radiolysis/releases/aq_radiolysis-0.1.2.tar.gz && \
    python3 -m pytest --pyargs aq_radiolysis && \
    python3 -m pip install http://hera.physchem.kth.se/~chemreac-derivations/chemreac-derivations-0.1.x/advediffreac-0.1.1.dev0%2bgit.tar.gz && \
    python3 -m pytest --pyargs advediffreac
