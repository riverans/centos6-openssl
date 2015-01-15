centos6-openssl
===============

Spec file for backport of OpenSSL 1.0.1j for CentOS 6

Simple Methods
==============

Someone other than me (ptudor) has added the FC srpm to the repo. It may make things simpler. Anyone can update this README and I (ptudor) will approve changes; the webpage at ptudor.net is my own free speech and is purely content owned and created by me. 


Quick Summary:
==============
You will need the following tools to build openssl
````
yum -y groupinstall "Development tools" 
yum -y install rpm-build zlib-devel krb5-devel
````

On a fresh install only root has access to /usr/srv/redhat
````
sudo mkdir /usr/src/redhat
sudo chown yourusername:yourusername /usr/src/redhat
mkdir -p /usr/src/redhat/{BUILD,RPMS,SOURCES,SPECS,SRPMS}

````
git clone https://github.com/ptudor/centos6-openssl.git && cd centos6-openssl
````

Download the openssl-1.0.1j from OpenSSL site and also copy all the SOURCES from this git to 
the rpmbuild's SOURCES dir and the spec file to SPECS dir (this is optional) and build it.

````
cp SOURCES/* /usr/src/redhat/SOURCES
cp openssl.spec /usr/src/redhat/SPECS
wget -O /usr/src/redhat/SOURCES/openssl-1.0.1j.tar.gz https://www.openssl.org/source/openssl-1.0.1j.tar.gz
cd /usr/src/redhat/SPECS && rpmbuild -ba openssl.spec
````

Now that rpmbuild has completed, we have some files to install.
````
cd /usr/src/redhat/RPMS/x86_64/
rpm -Fvh openssl-1.0.1j-*.rpm openssl-libs-1.0.1j-*.rpm openssl-devel-1.0.1j-*.rpm
````

Additional Information:
Confirm that it will work on both CentOS 6.5 and 6.6 -richbria
Confirming that this does not work on CentOS 7 - richbria

See also: 

https://www.ptudor.net/linux/openssl/

http://unix.stackexchange.com/questions/84283/how-can-i-get-tlsv1-2-support-in-apache-on-rhel6-centos-sl6/86326

http://www.centos.org/modules/newbb/viewtopic.php?topic_id=41784&forum=55&post_id=189679
