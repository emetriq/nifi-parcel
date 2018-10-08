NiFi Parcel
===========

This repository provides a parcel(https://github.com/cloudera/cm_ext) to install Apache NiFi as a service usable by Cloudera Manager.

## Overview
- Quick install
  - [below one this page](#quick-install)
- Build Parcel and CSD
  - [Build all](/howtos/build-all/)
- Howtos
  - [Setup SSL](/howtos/ssl/)
  - [Enable Ldap (Active Directory)](/howtos/ads-ldap/)
- Todos, finished features
  - [bottom of this page](#todos)

### Quick install
1. Download CSD [latest release](/emetriq/nifi-parcel/releases/latest)
```sh
$ cp NIFI-1.2.jar /opt/cloudera/csd
$ sudo service cloudera-scm-server restart
# Wait a min, go to Cloudera Manager -> Add a Service -> NiFi
```
2. Manually add a parcel download URL to cloudera CDH

  - :exclamation: TODO: There is currently no public download for the Nifi parcel available, see [Build all](/howtos/build-all/)
    ![CDH GUI - Parcel Config](Screenshot_20181008_182623.png)



## Todos
- [x] "Currently `NiFi` runs under the `root` user" 
  - done. User is *nifi*.
- [x] Expose config options under Cloudera Manager 
  - Conf folder from parcels is used, this needs to be migrated to ConfigWriter - done for all basic settings
- [ ] simplify install
  - [x] Provide precompiled CSD
    - see [latest release](/emetriq/nifi-parcel/releases/latest)
  - [ ] Provide parcel repo
  - [ ] Include parcel repo URL in CSD
- [ ] Expose metrics from NiFi in CDH
- [ ] Allow reading log files in CDH
- [x] https config
  - [x] document certificate Management
  - [ ] \(optional\) Puppet CA integration - blocked by https://tickets.puppetlabs.com/browse/SERVER-2338
- [x] Login
  - [x] this requires https
- [ ] Fix *WebUI* link in CDH
- [ ] Parcel building in Jenkins
  - [ ] Use Nifi releases
- [ ] multi distribution support for parcels
