FROM gns3/ipterm:latest
RUN apt-get update && apt-get -y install vim nano quagga quagga-doc bridge-utils iperf sudo 

RUN apt-get -y install ftp ftpd tftpd-hpa tftp-hpa 

RUN apt-get -y install tftp vsftpd xinetd tftpd 

RUN cp /usr/share/doc/quagga/examples/zebra.conf.sample /etc/quagga/zebra.conf \
 && cp /usr/share/doc/quagga/examples/ripd.conf.sample /etc/quagga/ripd.conf \
 && cp /usr/share/doc/quagga/examples/ospfd.conf.sample /etc/quagga/ospfd.conf \
 && cp /usr/share/doc/quagga/examples/bgpd.conf.sample /etc/quagga/bgpd.conf \
 && cp /usr/share/doc/quagga/examples/vtysh.conf.sample /etc/quagga/vtysh.conf \
 && sed -i "s/zebra=no/zebra=yes/" /etc/quagga/daemons \
 && sed -i "s/ripd=no/ripd=yes/" /etc/quagga/daemons \
 && sed -i "s/ospfd=no/ospfd=yes/" /etc/quagga/daemons \
 && sed -i "s/bgpd=no/bgpd=yes/" /etc/quagga/daemons

RUN sed -i "s/anonymous_enable=NO/anonymous_enable=YES/" /etc/vsftpd.conf \
 && sed -i "s/#write_enable/write_enable/" /etc/vsftpd.conf \
 && sed -i "s/n=0/sleep 1; n=0/" /etc/init.d/vsftpd \
 && sed -i "s/local_enable=YES/local_enable=NO/" /etc/vsftpd.conf \
 && echo "no_anon_password=YES" >> /etc/vsftpd.conf

RUN cp /etc/default/tftpd-hpa /etc/default/tftpd-hpa.ORIGINAL

RUN apt-get -y install telnetd

RUN apt-get -y install iptables isc-dhcp-server isc-dhcp-client


RUN mkdir lab8 && apt-get -y install bind9 bind9utils dnsutils

RUN sed -i "s/hosts: files dns/ hosts: dns files/" /etc/nsswitch.conf 

RUN useradd -ms /bin/bash labuser -G sudo
RUN echo "NWrks@el\nNWrks@el" | passwd labuser
RUN echo "labuser ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers 
USER labuser
WORKDIR /home/labuser

COPY NamedConfPC*.tar.gz lab8/
COPY named-installPC* lab8/


