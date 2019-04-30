FROM bjodah/bjodahimg18:v1.8
MAINTAINER Björn Dahlgren <bjodah@DELETEMEgmail.com>
ENV CC=gcc-8 \
    CXX=g++-8 \
    CPLUS_INCLUDE_PATH=/opt/boost_1_70_0/include:/opt/sundials-3.2.1-klu-lapack/include \
    LIBRARY_PATH=/opt/sundials-3.2.1-klu-lapack/lib \
    LD_LIBRARY_PATH=/opt/sundials-3.2.1-klu-lapack/lib

RUN cd /tmp && curl -Ls https://github.com/symengine/symengine.py/archive/v0.4.0.tar.gz | tar xz && \
    cd symengine.py-0.4.0 && python3 setup.py install --symengine-dir=/opt/symengine-0.4.0 && cd .. && rm -r symengine.py-* && \
    python3 -c 'import symengine; assert symengine.test()' && \
      python3 -m pip install --upgrade "pyodeint>=0.9.8,<0.10.0" "pygslodeiv2>=0.8.4,<0.9.0" "pycvodes>=0.10.16,<0.11.0" "pycodeexport>=0.1.2,<0.2.0" "pycompilation>=0.4.3,<0.5.0" notebook pygraphviz "pykinsol>=0.1.3" && \
    python3 -m pytest --pyargs pyodeint && \
    python3 -m pytest --pyargs pygslodeiv2 && \
    python3 -m pytest --pyargs pycvodes && \
    python3 -m pytest --pyargs pykinsol && \
    python3 -m pip install --upgrade "pyneqsys>=0.5.6" "pyodesys>=0.11.19,<0.12.0" "block_diag_ilu>=0.3.9,<0.4.0" "finitediff>=0.6.2" && \
    python3 -m pytest --pyargs pyneqsys && \
    python3 -m pytest --pyargs pyodesys && \
    python3 -m pip install "chempy>=0.6.18,<0.7.0" && \
    python3 -m pytest --pyargs chempy && \
    python3 -m pip install "chemreac>=0.7.15,<0.8.0" && \
    python3 -m pytest --pyargs chemreac && \
    python3 -m pip install http://hera.physchem.kth.se/~kinetgine/releases/pykinetgine-0.3.5.tar.gz && \
    python3 -m pytest --pyargs pykinetgine && \
    python3 -m pip install http://hera.physchem.kth.se/~aq_radiolysis/releases/aq_radiolysis-0.1.4.tar.gz && \
    python3 -m pytest --pyargs aq_radiolysis && \
    python3 -m pip install http://hera.physchem.kth.se/~chemreac-derivations/releases/advediffreac-0.1.3.tar.gz && \
    python3 -m pytest --pyargs advediffreac && \
    python3 -m pip install http://hera.physchem.kth.se/~batemaneq/releases/batemaneq-0.2.0.tar.gz && \
    python3 -m pytest --pyargs batemaneq && \
    rm -rf ~/.cache/pip
