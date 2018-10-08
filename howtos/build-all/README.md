Building NiFi Parcel and CSD
============================

This repository provides a parcel(https://github.com/cloudera/cm_ext) to install Apache NiFi as a service usable by Cloudera Manager.

# Overview
0. Install `cloudera/cm_ext`
1. Create parcel + CSD
2. Publish parcel
3. Publish CSD

# Build and install parcel + CSD
Besides this repository we also need the Cloudera Manager repo for CSD validation. The we can build a parcel and a CSD
##  Install Steps
### Install Prerequisites: `cloudera/cm_ext`
```sh
git clone https://github.com/cloudera/cm_ext
cd cm_ext/validator
mvn install
```

### Build parcel
- variant(a) build nifi manually
```sh
# First, create NiFi package
$ git clone http://github.com/apache/nifi
$ cd nifi
$ mvn clean install
$ cd /tmp
$ git clone http://github.com/emetriq/nifi-parcel
$ cd nifi-parcel
$ POINT_VERSION=5 VALIDATOR_DIR=../cm_ext ./build-parcel.sh /tmp/nifi/nifi-assembly/target/nifi-*-SNAPSHOT-bin.tar.gz
```

- variant (b) use prebuild nifi package
```sh
# First, download NiFi package
$ sha265sum nifi-1.7.1-bin.tar.gz
# 14441c02c47541981746adc8a6c5d8759a9bf8324a08bc03c8487b1112e2c515
$ git clone http://github.com/emetriq/nifi-parcel
$ cd nifi-parcel
$ POINT_VERSION=5 VALIDATOR_DIR=../cm_ext ./build-parcel.sh ../nifi-*-bin.tar.gz
```

###  Create CSD
```sh
$ cd nifi-parcel
$ VALIDATOR_DIR=../cm_ext ./build-csd.sh
```

###  Move CSD to Cloudera Manager's CSD Repo
```sh
# transfer build-csd/NIFI-1.0.jar to CM's host
$ cp NIFI-1.0.jar /opt/cloudera/csd
$ sudo service cloudera-scm-server restart
# Wait a min, go to Cloudera Manager -> Add a Service -> NiFi
```


### Serve Parcel using Python
```sh
$ cd build-parcel
$ python -m SimpleHTTPServer 14641
# navigate to Cloudera Manager -> Parcels -> Edit Settings
# Add fqdn:14641 to list of urls
# install the NIFI parcel
```
