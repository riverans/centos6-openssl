centos6-openssl
===============

Spec file for backport of OpenSSL 1.0.1j for CentOS 6


Simple Methods
==============

Someone other than me (ptudor) has added the FC srpm to the repo. It may make things simpler. Anyone can update this README and I (ptudor) will approve changes; the webpage at ptudor.net is my own free speech and is purely content owned and created by me. 


Quick Summary:
==============
Assuming you have built an RPM before and also have git, download this repository

````
git clone https://github.com/ptudor/centos6-openssl.git && centos6-openssl
````

Download the openssl-1.0.1j from OpenSSL site and also copy all the SOURCES from this git to 
the rpmbuild's SOURCES dir and the spec file to SPECS dir (this is optional) and build it.

````
cp SOURCES/* /usr/src/redhat/SOURCES
cp openssl.spec /usr/src/redhat/SPECS
wget -O /usr/src/redhat/SOURCES/openssl-1.0.1j.tar.gz https://www.openssl.org/source/openssl-1.0.1j.tar.gz
cd /usr/src/redhat/SPECS && rpmbuild -ba openssl.spec
````

See also: 

https://www.ptudor.net/linux/openssl/

http://unix.stackexchange.com/questions/84283/how-can-i-get-tlsv1-2-support-in-apache-on-rhel6-centos-sl6/86326

http://www.centos.org/modules/newbb/viewtopic.php?topic_id=41784&forum=55&post_id=189679
