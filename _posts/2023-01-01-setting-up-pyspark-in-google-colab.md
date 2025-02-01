---
layout: post
---

*Note: Newer versions of libraries are available*

Google Colab is an amazing tool based on Jupyter Notebooks. The most attractive feature of Colab is the free support of GPU and TPU it comes with. With GPU support running on Google’s own servers, it is actually faster than commercially available GPUs like the Nvidia 1050Ti.


Apache Spark is an in-memory data analytics engine. It is wildly popular with data scientists because of its speed, scalability and ease-of-use. PySpark has a way to handle parallel processing without the need for the threading or multiprocessing modules. Learn more about Pyspark here:


To run spark in Colab, first we need to install all the dependencies in Colab environment such as Apache Spark with hadoop, Java 8 and Findspark in order to locate the spark in the system.


Follow the code to install the dependencies:
```
!apt-get install openjdk-8-jdk-headless -qq > /dev/null
!wget -q https://www-eu.apache.org/dist/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz
!tar -xvzf spark-2.4.4-bin-hadoop2.7.tgz
!pip install -q findspark
```

It is now time to set the environment path that enables us to run PySpark in our Colab environment. Set the location of Java and Spark by running the following code:
```
import os
os.environ[“JAVA_HOME”] = “/usr/lib/jvm/java-8-openjdk-amd64”
os.environ[“SPARK_HOME”] = “/content/spark-2.3.2-bin-hadoop2.7”
```

We can run a local spark session to test our installation:
```
import findspark
findspark.init("spark-2.4.4-bin-hadoop2.7")
from pyspark.sql import SparkSession
spark = SparkSession.builder.master("local[*]").getOrCreate()
spark
```
The spark keyword on the above code initiates local spark session.
![spark session](https://imgur.com/a/xeST6kS){:.ioda}

Congras, you can now run and use PySpark in Google Colab. Happy Analytics.