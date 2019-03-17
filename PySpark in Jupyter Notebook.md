# This document lists out the steps required to install and run PySpark in Jupyter Notebook on Windows 10.

## 1. Requirements
- Spark distribution from https://spark.apache.org/downloads.html
- Python
- Jupyter Notebook
- winutils.exe - a Hadoop binary for Windows - from Steve Loughran’s [GitHub repo](https://github.com/steveloughran/winutils/). Go to the corresponding Hadoop version in the Spark distribution and find winutils.exe under /bin
- The *findspark* module. It can be installed by running *python -m pip install findspark* in the Command prompt or Git bash.
- Java
** Use 7-zip to unpack the .tgz file

## 2. Installation
- Unpack the .tgz file in a separate folder. (eg: C:\spark\spark-2.4.0-bin-hadoop2.7)
- Move the winutils.exe to the \bin folder of Spark distribution.
- Add the below environment variables:

| Name                        | Value                               |
| --------------------------- | ----------------------------------- |
| SPARK_HOME                  | C:\spark\spark-2.4.0-bin-hadoop2.7  |
| HADOOP_HOME                 | C:\spark\spark-2.4.0-bin-hadoop2.7  |
| PYSPARK_DRIVER_PYTHON       | jupyter                             |
| PYSPARK_DRIVER_PYTHON_OPTS  | notebook                            |

- Add C:\spark\spark-2.4.0-bin-hadoop2.7\bin to the path in system variables

## 3. Running PySpark in Jupyter Notebook
- Open jupyter notebook and run the following code:
```
import findspark
findspark.init('C:\spark\spark-2.4.0-bin-hadoop2.7')

import pyspark
from pyspark.sql import SparkSession

spark = SparkSession.builder.getOrCreate()

df = spark.sql('''select 'spark' as hello ''')
df.show()
```
- Once you see the following output, then you have installed PySpark on Windows.
```
+-----+
|hello|
+-----+
|spark|
+-----+

```
    
Reference: https://changhsinlee.com/install-pyspark-windows-jupyter/
