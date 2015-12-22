FROM ubuntu:trusty

RUN apt-get update
RUN apt-get -y install git subversion gcc clang cmake wget gfortran

RUN cd /var
RUN svn checkout --non-interactive --trust-server-cert https://projects.coin-or.org/svn/SYMPHONY/releases/5.6.13 /var/symphony
RUN cd /var/symphony/ThirdParty/Glpk && ./get.Glpk
RUN cd /var/symphony && ./configure &&  make -j4 && make install
