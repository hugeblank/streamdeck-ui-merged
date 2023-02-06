Installing on CentOS
====================

The following guide was tested on CentOS 7.

Add the following repositry. This is needed because **hidapi** does not exist in the standard repo.

``` console
sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

Install **hidapi**

``` console
sudo yum install hidapi
```
Streamdeck-ui has a dependency on Python 3.8, but CentOS 7 only supports Python 3.6.
The following steps will build Python 3.8 ([source](https://computingforgeeks.com/how-to-install-python-3-on-centos/)).

``` console
sudo yum -y groupinstall "Development Tools"
sudo yum -y install openssl-devel bzip2-devel libffi-devel
wget https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz
tar xvf Python-3.8.3.tgz
cd Python-3.8.3/
./configure --enable-optimizations
sudo make altinstall
```
This should now work
``` console
python3.8 --version
```
Install all the dependencies
``` console
pip3.8 install streamdeck-ui --user
PATH=$PATH:$HOME/.local/bin
```

We need configure the USB device to be accessible by the currently logged in user, when it is attached:
``` console
sudo nano /etc/udev/rules.d/70-streamdeck.rules
SUBSYSTEM=="usb", ATTRS{idVendor}=="0fd9", TAG+="uaccess"
```
Remove and plug your Stream Deck in.
``` console
streamdeck
```
