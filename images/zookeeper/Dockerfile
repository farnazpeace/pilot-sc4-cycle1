# Dockerfile for Zookepeer customized for the BDE SC4 Pilot 
#
# 1) Build an image using this docker file. Run the following docker command
#
#    $ docker build -t bde2020/pilot-sc4-zookeeper:v0.0.1 .
#
# 2) Test the Kafka producer for the FCD data  in a container. Run the following
#    command
#
#    $ docker run --rm -it --name zookeeper  bde2020/pilot-sc4-zookeeper:v0.0.1
#
#    The option --add-host tells docker to add kafkahost to /etc/hosts file so $
#    in the bootstrap.servers=kafkahost:9092 can be resolved. This configuratio$
#    container and Kafka runs on the host.
#    The Kafka broker, to which the producers send the data, must be configured$
#    host network address assigned to it by docker, that is docker0 (not eth0).$
#    to the address 172.17.0.1 then in the server.properties file used to start$
#    listeners=PLAINTEXT://172.17.0.1:9092   
#
# 3) Start a container in daemon mode
#
#    $ docker run -d --name fcd-producer bde2020/pilot-sc4-fcd-producer:v0.0.1 
#
# Pull the base image
FROM bde2020/zookeeper

MAINTAINER Luigi Selmi <luigiselmi@gmail.com>

# Install  network tools (ifconfig, netstat, ping, ip)
RUN apt-get update && \
    apt-get install -y net-tools && \
    apt-get install -y iputils-ping && \
    apt-get install -y iproute2

# Add the Zookeeper configuration file
ADD zoo.cfg /config/
ADD zoo_replicated1.cfg.dynamic /config/

# Start Zookeeper
ADD start_zookeeper.sh /
#RUN ["sh", "start_zookeeper.sh"]
