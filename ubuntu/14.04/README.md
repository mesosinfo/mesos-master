mesos-master

[![](https://badge.imagelayers.io/mesosinfo/mesos-master:ubuntu-14.04.svg)](https://imagelayers.io/?images=mesosinfo/mesos-master:ubuntu-14.04 'Get your own badge on imagelayers.io')

===========================================================
Multi-node Setup

For this setup, we will need 3 servers with Docker installed on it.

1. Export out the 3 servers' IP that we will be using on each server

		#zookeeper servers
        ZOOKEEPER_HOST_IP_1=192.168.22.82
        ZOOKEEPER_HOST_IP_2=192.168.22.87
        ZOOKEEPER_HOST_IP_3=192.168.22.92

		#Mesos master servers
		MASTER_IP_1=192.168.22.96
		MASTER_IP_2=192.168.22.93
		MASTER_IP_3=192.168.22.84

		 
2. Run the mesos masters on docker

    On host #1

		docker run --net="host" \
		-p 5050:5050 \
		-e "MESOS_HOSTNAME=${MASTER_IP_1}" \
		-e "MESOS_IP=${MASTER_IP_1}" \
		-e "MESOS_ZK=zk://${ZOOKEEPER_HOST_IP_1}:2181,${ZOOKEEPER_HOST_IP_2}:2181,${ZOOKEEPER_HOST_IP_3}:2181/mesos" \
		-e "MESOS_PORT=5050" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_QUORUM=1" \
		-e "MESOS_REGISTRY=in_memory" \
		-e "MESOS_WORK_DIR=/var/lib/mesos" \
		-d \
		mesosinfo/mesos-master


    On host #2

		docker run --net="host" \
		-p 5050:5050 \
		-e "MESOS_HOSTNAME=${MASTER_IP_2}" \
		-e "MESOS_IP=${MASTER_IP_2}" \
		-e "MESOS_ZK=zk://${ZOOKEEPER_HOST_IP_1}:2181,${ZOOKEEPER_HOST_IP_2}:2181,${ZOOKEEPER_HOST_IP_3}:2181/mesos" \
		-e "MESOS_PORT=5050" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_QUORUM=1" \
		-e "MESOS_REGISTRY=in_memory" \
		-e "MESOS_WORK_DIR=/var/lib/mesos" \
		-d \
		mesosinfo/mesos-master

    On host #3

		docker run --net="host" \
		-p 5050:5050 \
		-e "MESOS_HOSTNAME=${MASTER_IP_3}" \
		-e "MESOS_IP=${MASTER_IP_3}" \
		-e "MESOS_ZK=zk://${ZOOKEEPER_HOST_IP_1}:2181,${ZOOKEEPER_HOST_IP_2}:2181,${ZOOKEEPER_HOST_IP_3}:2181/mesos" \
		-e "MESOS_PORT=5050" \
		-e "MESOS_LOG_DIR=/var/log/mesos" \
		-e "MESOS_QUORUM=1" \
		-e "MESOS_REGISTRY=in_memory" \
		-e "MESOS_WORK_DIR=/var/lib/mesos" \
		-d \
		mesosinfo/mesos-master
		
