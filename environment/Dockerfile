FROM bjodah/bjodahimg18:v1.3
MAINTAINER Björn Dahlgren <bjodah@DELETEMEgmail.com>
RUN apt-get update && \
    apt-get --quiet --assume-yes install libsundials-dev && \    
    python3 -m pip uninstall sympy && \
    python3 -m pip install --upgrade pyodeint>=0.9.8,<0.10.0 pygslodeiv2>=0.8.4,<0.9.0 pycvodes>=0.10.8,0.11.0 pyodesys>=0.11.16,<0.12.0 sympy>=1.1.1,!=1.2 block_diag_ilu>=0.3.9,<0.4.0 chemreac>=0.7.10,<0.8.0 chempy>=0.6.8,<0.7.0 && \
    python3 -m pytest --pyargs pyodesys --slow --veryslow
