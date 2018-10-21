FROM java:openjdk-8-jdk

ARG spark_ver=2.2.2

RUN apt-get update -y && \
    apt-get install -y scala python3 python3-dev \
    python3-pip python3-numpy python3-scipy python3-pandas gfortran && \
    pip3 install --upgrade pip && \
    rm -rf /var/lib/apt/lists/*
# Get Spark from apache mirror.
RUN mkdir -p /opt && \
    cd /opt && \
    wget http://apache.mirrors.pair.com/spark/spark-${spark_ver}/spark-${spark_ver}-bin-hadoop2.7.tgz && \
    tar -zvxf spark-${spark_ver}-bin-hadoop2.7.tgz && \
    rm spark-${spark_ver}-bin-hadoop2.7.tgz && \
    ln -s spark-${spark_ver}-bin-hadoop2.7 spark && \
    mkdir /opt/spark/logs && \
    echo Spark installed in /opt && \
    apt remove wget -y && \
    apt-get autoremove -y
COPY log4j.properties /opt/spark/conf/log4j.properties
COPY setup_client.sh start-master.sh start-worker.sh  /
RUN  chmod +x /start-*

EXPOSE 7077 4040 8080

ENV SPARK_HOME=/opt/spark \
    JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 \
    JRE_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre \
    PYTHONPATH=/opt/spark/python \
    PYSPARK_PYTHON=python3 \
    PATH=$PATH:/opt/spark/bin:~/.local/bin:/usr/lib/jvm/java-8-oracle/bin:/usr/lib/jvm/java-8-oracle/jre/bin


#RUN cd /opt/spark/jars && \
#    wget http://central.maven.org/maven2/org/apache/kafka/kafka_2.12/2.0.0/kafka_2.12-2.0.0.jar && \
#    wget http://central.maven.org/maven2/org/apache/kafka/kafka-clients/2.0.0/kafka-clients-2.0.0.jar && \
#    wget http://central.maven.org/maven2/org/apache/spark/spark-streaming-kafka-0-10_2.11/2.2.2/spark-streaming-kafka-0-10_2.11-2.2.2.jar && \
#    wget http://central.maven.org/maven2/org/apache/spark/spark-streaming-kafka-0-8_2.11/2.2.2/spark-streaming-kafka-0-8_2.11-2.2.2.jar && \
#    echo maven jars installed in /opt/spark/jars

    
