# docker-deops


#!/bin/bash
ps -ef|grep yz-cp-back-boot-0.0.1-SNAPSHOT.jar | awk {'print $2'} | xargs kill
nohup java -jar yz-cp-back-boot-0.0.1-SNAPSHOT.jar >front-`date +%F`.log 2>&1 &
