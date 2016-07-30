FROM ubuntu:latest
MAINTAINER Ted Ralphs <ted@lehigh.edu>

RUN apt-get update
RUN apt-get -y install git subversion gcc clang cmake wget gfortran

RUN cd /var
RUN svn checkout --non-interactive --trust-server-cert https://projects.coin-or.org/svn/CoinBinary/OptimizationSuite/stable/1.8 /var/coin-or
RUN cd /var/coin-or && ./get.AllThirdParty
RUN cd /var/coin-or && ./configure --with-gmpl --enable-gnu-packages &&  make -j4 && make install
