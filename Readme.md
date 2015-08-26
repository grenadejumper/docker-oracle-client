# docker-oracle-client

A docker-container for Oracle Instant Client 12, based on CentOs. Perfect for using together with a dockerized oracle database, for instance [this one](https://github.com/biemond/docker-database-puppet).

## Step 1

Unfortunately, Oracle does not allow us to include their software in docker-images, so you need to download Oracle Instant Client linux binaries (and accept their license) before we build the image. 

Get the following files 

* oracle-instantclient12.1-basic-12.1.0.2.0-1.rpm
* oracle-instantclient12.1-devel-12.1.0.2.0-1.rpm
* oracle-instantclient12.1-sqlplus-12.1.0.2.0-1.rpm

from [here](http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html)

Place the files in the same directory as the Dockerfile.

## Step 2 (optional)
Edit the included tnsnames.ora file, so you can conveniently access these databases from the container, without having to enter the entire connection string. 

## Step 3 
Build the image

`docker build -t oracle/oracleclient .`

## Step 4
Run the image. If you are running a dockerized database, pass its reference in via a docker link:

`docker run --it --name oracleclient --link oracle:oracle oracle/oracleclient`

Otherwise, you can run it without the link, and connect to other databases via a connection string.

`docker run --it --name oracleclient oracle/oracleclient`

## Step 5
Verify that it works

`sqlplus sys/Welcome01@oracle`
