FROM apache/zeppelin:0.8.0
ARG spark_ver=2.2.2

RUN cd /opt && \
    wget http://apache.mirrors.pair.com/spark/spark-${spark_ver}/spark-${spark_ver}-bin-hadoop2.7.tgz && \
    tar -zvxf spark-${spark_ver}-bin-hadoop2.7.tgz && \
    rm spark-${spark_ver}-bin-hadoop2.7.tgz && \
    ln -s spark-${spark_ver}-bin-hadoop2.7 spark && \
    mkdir /opt/spark/logs && \
    echo Spark installed in /opt && \
    apt remove wget -y && \
    apt-get autoremove -y
COPY interpreter.json configuration.xsl  /zeppelin/conf/

RUN pip install --upgrade pip && \
    pip install pyspark 
