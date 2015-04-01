centos6-openssl
===============

Spec file for backport of OpenSSL 1.0.1k for CentOS 6

Simple Methods
==============

Someone other than me (ptudor) has added the FC srpm to the repo. It may make things simpler. Anyone can update this README and I (ptudor) will approve changes; the webpage at ptudor.net is my own free speech and is purely content owned and created by me. 


Quick Summary:
==============
You will need the following tools to build openssl
````
yum -y groupinstall "Development tools" 
yum -y install rpm-build zlib-devel krb5-devel buildsys-macros
````
On a fresh install only root has access to /usr/srv/redhat so lets fix it
````
sudo mkdir /usr/src/redhat
sudo chown yourusername:yourusername /usr/src/redhat
mkdir -p /usr/src/redhat/{BUILD,RPMS,SOURCES,SPECS,SRPMS}
````
Clone this repository
````
git clone https://github.com/ptudor/centos6-openssl.git && cd centos6-openssl
````
Copy all the SOURCES from this git to the rpmbuild's SOURCES dir and the spec file to SPECS dir (this is optional) and build it.
````
cp SOURCES/* /usr/src/redhat/SOURCES
cp openssl.spec /usr/src/redhat/SPECS
````
Download openssl-1.0.1k from OpenSSL site
````
wget -O /usr/src/redhat/SOURCES/openssl-1.0.1k.tar.gz https://www.openssl.org/source/openssl-1.0.1k.tar.gz
````
Build your RPM
````
cd /usr/src/redhat/SPECS && rpmbuild -ba openssl.spec
````
Now that rpmbuild has completed, we have some files to install.
````
cd /usr/src/redhat/RPMS/x86_64/
rpm -Fvh openssl-1.0.1k-*.rpm openssl-libs-1.0.1k-*.rpm openssl-devel-1.0.1k-*.rpm
````
Let’s make sure it works by listing supported TLS ciphers
````
openssl ciphers -v 'TLSv1.2' | head -4
````
Without ECC your output will look like:
````
DHE-DSS-AES256-GCM-SHA384 TLSv1.2 Kx=DH Au=DSS Enc=AESGCM(256) Mac=AEAD
DHE-RSA-AES256-GCM-SHA384 TLSv1.2 Kx=DH Au=RSA Enc=AESGCM(256) Mac=AEAD
DHE-RSA-AES256-SHA256 TLSv1.2 Kx=DH Au=RSA Enc=AES(256) Mac=SHA256
DHE-DSS-AES256-SHA256 TLSv1.2 Kx=DH Au=DSS Enc=AES(256) Mac=SHA256
````
With ECC your output will look like:
````
ECDHE-RSA-AES256-GCM-SHA384 TLSv1.2 Kx=ECDH Au=RSA Enc=AESGCM(256) Mac=AEAD
ECDHE-ECDSA-AES256-GCM-SHA384 TLSv1.2 Kx=ECDH Au=ECDSA Enc=AESGCM(256) Mac=AEAD
ECDHE-RSA-AES256-SHA384 TLSv1.2 Kx=ECDH Au=RSA Enc=AES(256) Mac=SHA384
ECDHE-ECDSA-AES256-SHA384 TLSv1.2 Kx=ECDH Au=ECDSA Enc=AES(256) Mac=SHA384
````

Additional Information:
==============
Confirming that it will work on both CentOS 6.5 and 6.6 -richbria
Confirming that this does not work on CentOS 7 - richbria

See also: 

https://www.ptudor.net/linux/openssl/

http://unix.stackexchange.com/questions/84283/how-can-i-get-tlsv1-2-support-in-apache-on-rhel6-centos-sl6/86326

http://www.centos.org/modules/newbb/viewtopic.php?topic_id=41784&forum=55&post_id=189679
