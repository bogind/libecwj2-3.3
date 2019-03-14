# libecwj2-3.3
storage and installation instruction for libecwj2 version 3.3 which released on June 9th 2006

## Installation on Ubuntu (Tested on 16.04)
### for a manual configuration of gdal
### Installing libecwj2
```
$ sudo apt install g++ build-essential autoconf automake m4 libtool gcc make unzip wget libgdal1-dev swig ant
# wget https://s3-ap-southeast-2.amazonaws.com/adamogradybackups/libecwj2-3.3-2006-09-06.zip #Or
# wget https://github.com/bogind/libecwj2-3.3/raw/master/libecwj2-3.3-2006-09-06.zip
# unzip libecwj2-3.3-2006-09-06.zip
# wget http://trac.osgeo.org/gdal/raw-attachment/ticket/3162/libecwj2-3.3-msvc90-fixes.patch
# patch -p0< libecwj2-3.3-msvc90-fixes.patch
# wget http://osgeo-org.1560.x6.nabble.com/attachment/5001530/0/libecwj2-3.3-wcharfix.patch
# wget http://trac.osgeo.org/gdal/raw-attachment/ticket/3366/libecwj2-3.3-NCSPhysicalMemorySize-Linux.patch
# cd libecwj2-3.3
# patch -p0< ../libecwj2-3.3-NCSPhysicalMemorySize-Linux.patch
# patch -p1< ../libecwj2-3.3-wcharfix.patch
$ ./configure
$ sudo make
$ sudo make install
```

## Getting and installing GDAL 2.2.2
```
# wget -c http://download.osgeo.org/gdal/2.2.2/gdal-2.2.2.tar.gz
# tar -xvzf gdal-2.2.2.tar.gz
# cd gdal-2.2.2
```
**NOTE** I recommend configuring and installing with java bindings as well curl, postgres, python and spatialite.
If you only want ECW support you can drop all the other flags after it.
As for the java bindings, these worked best for me with java-8-oracle and not with openjdk
```
$ ./configure --with-ecw=/usr/local --with-python --with-spatialite --with-pg --with-curl --with-java=/usr/lib/jvm/java-8-oracle --with-jvm-lib=/usr/lib/jvm/java-8-oracle/jre/lib/amd64/server --with-jvm-lib-add-rpath=yes
```
Make sure you see ECW support marked as yes on the list
```
$ sudo make
$ sudo make install
```
After dinishing this you need to set the PATH and LD_LIBRARY_PATH environment variables so that GDAL could recognise the location of the ECW library (bu default /usr/local/lib).
The easiest way i found to doing this is:
```
$ echo 'export LD_LIBRARY_PATH=/usr/local/lib' >> ~/.profile
$ echo 'export LD_LIBRARY_PATH=/usr/local/lib' >> ~/.bashrc
sudo ldconfig
```
Add the following rows to `/etc/enviroment`
```
GDAL_DATA="/usr/local/share/gdal"
PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"
JAVA_HOME="/usr/lib/jvm/java-8-oracle"
```

# Testing the installation was succefull
on Linux open a terminal
```
gdalinfo --formats | grep ECW
```
On Windows open CMD
```
gdalinfo --formats | findstr ECW
```

# TODO
 -  Add section about installing on windows
