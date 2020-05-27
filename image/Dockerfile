FROM ubuntu:xenial
MAINTAINER Ted Ralphs <ted@lehigh.edu>

RUN apt-get update
RUN apt-get -y install --no-install-recommends git subversion gcc g++ make wget gfortran patch pkg-config file
RUN apt-get -y install --no-install-recommends libgfortran-5-dev libblas-dev liblapack-dev libmetis-dev libnauty2-dev
RUN apt-get -y install --no-install-recommends ca-certificates

RUN git clone https://github.com/coin-or/coinbrew /var/coin-or
WORKDIR /var/coin-or
RUN ./coinbrew fetch COIN-OR-OptimizationSuite@stable/1.9 --skip="ThirdParty/Blas ThirdParty/Lapack ThirdParty/Metis" --no-prompt
RUN ./coinbrew build  COIN-OR-OptimizationSuite --skip="ThirdParty/Blas ThirdParty/Lapack ThirdParty/Metis" --no-prompt --prefix=/usr
