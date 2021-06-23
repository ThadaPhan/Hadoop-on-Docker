FROM ubuntu
MAINTAINER 18133006@student.hcmute.edu.vn
RUN apt update && apt install -y openssh-server openssh-client vim openjdk-8-jdk
RUN apt update && apt install -y git

# SSH
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
RUN sed -ri 's/#   StrictHostKeyChecking ask/    StrictHostKeyChecking accept-new/g' /etc/ssh/ssh_config
RUN chmod 0600 ~/.ssh/authorized_keys

RUN echo "root:123" | chpasswd
RUN echo "root   ALL=(ALL)       ALL" >> /etc/sudoers

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV PATH $JAVA_HOME/bin:$PATH

#SCALA
RUN wget https://downloads.lightbend.com/scala/2.12.3/scala-2.12.3.deb
RUN dpkg -i scala-2.12.3.deb
RUN apt update && apt install -y scala

#SBT
RUN apt update && apt install -y gnupg2
RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
RUN apt update && apt install -y sbt

#SPARK 
RUN wget https://downloads.apache.org/spark/spark-3.0.2/spark-3.0.2-bin-hadoop2.7.tgz
RUN tar xvf spark-*
RUN mv spark-3.0.2-bin-hadoop2.7 usr/local/spark
ENV SPARK_HOME /usr/local/spark
ENV PATH $SPARK_HOME/bin:$PATH
ENV PATH $SPARK_HOME/sbin:$PATH
ENV PYSPARK_PYTHON usr/bin/python3

#KAFKA
RUN wget https://downloads.apache.org/kafka/2.6.2/kafka_2.13-2.6.2.tgz
RUN tar xzf kafka_2.13-2.6.2*
RUN mv kafka_2.13-2.6.2 usr/local/kafka
ADD config/server.properties usr/local/kafka/config/server.properties
ADD config/zookeeper.service /etc/systemd/system/zookeeper.service
ADD config/kafka.service     /etc/systemd/system/kafka.service




EXPOSE 22
