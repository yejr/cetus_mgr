## Introduction
Cetus is a high performance, stable, protocol aware proxy for MySQL Group Replication. 

## Getting started

### 1. Prerequisites
1. cmake
2. gcc
3. glib2-devel （version >= 2.6.0)
4. zlib-devel
5. flex
6. mysql-devel 5.6 or mysql-devel 5.7 or mariadb-devel
7. jemalloc

### 2. How to compile
1. Go to the cetus_mgr directory
2. mkdir build/
3. cd build/
4. CFLAGS='-O2 -w' cmake ../ -DCMAKE_BUILD_TYPE=Release -DCMAKE_EXE_LINKER_FLAGS="-ljemalloc" -DCMAKE_INSTALL_PREFIX=/home/user/cetus_mgr_install

### 3. How to install
make install

### 4. How to run
1. Go to /home/user/cetus_mgr_install/conf
2. cp proxy.conf.example proxy.conf
3. Modify proxy.conf 
4. cp users.json.example users.json
5. Modify users.json
6. Start Cetus `cd /home/user/cetus_mgr_install; ./bin/cetus --defaults-file=conf/proxy.conf --user=root --default-username=cetus_app`

### 5. How to modify proxy.conf
1. Modify proxy-backend-addresses to be the primary address of MySQL Group Replication
2. Modify proxy-read-only-backend-addresses to be the secondary addresses of MySQL Group Replication
3. Modify default-username to be the valid user name that could have the privileges of both manipulating MySQL Group Replication and MySQL.
4. Modify log-file to be the valid file path.
5. Modify worker-processes to be appropriate number that best suits the workload.
6. Modify default-pool-size appropriately.
7. Add group_replication_group_name appropriately.
8. Add group-replication-mode=1 for single primary mode.
9. Add backend-multi-write=true for multiple primary mode.
10. Add session-causal-read=true for session causal reading under session_track_gtids=OWN_GTID in MySQL conf settings.

### 6. How to modify user.conf
Modify password appropriately for both your applications and MySQL.

## Note
1. Cetus runs only on Linux.
2. Cetus could not be compiled under MySQL 8.0 development.
3. Cetus only works for MySQL Group Replication.
4. Cetus only supports mysql_native_password.
5. As for MySQL Group Replication, please use the modified version which could be downloaded at https://github.com/session-replay-tools/MySQL.
6. RESET MASTER before runing MySQL Group Replication
7. Make sure all of the MySQL Group Replication members is online before running cetus.
8. The total num of connections to each MySQL is equal to default-pool-size plus worker-processes.

## Bugs and feature requests:
If you encounter any issues with the release, I would encourage you to file a bug report.
Your feedback is really critical to myself and the rest of the team as we want to make cetus better.

