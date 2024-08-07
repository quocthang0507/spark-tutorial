# Installation

It is better to install Spark into a Linux based system.

## Step 1: Installing Java

First update your `apt` package index:

```bash
sudo apt update
```

Next, check if Java is already installed:

```bash
java -version
```

If Java is not currently installed, you'll get the following output:

```text
Command 'java' not found, but can be installed with:
sudo apt install openjdk-17-jre-headless  # version 17.0.8.1+1~us1-0ubuntu1~23.04, or
sudo apt install default-jre              # version 2:1.17-74
sudo apt install openjdk-11-jre-headless  # version 11.0.20.1+1-0ubuntu1~23.04
sudo apt install openjdk-20-jre-headless  # version 20.0.2+9+ds1-0ubuntu1~23.04
sudo apt install openjdk-8-jre-headless   # version 8u382-ga-1~23.04.1
sudo apt install openjdk-18-jre-headless  # version 18.0.2+9-2ubuntu1
sudo apt install openjdk-19-jre-headless  # version 19.0.2+7-0ubuntu4
sudo apt install openjdk-21-jre-headless  # version 21~14ea~us1-0ubuntu1
```

So you must install the JRE from OpenJDK:

```bash
sudo apt install default-jre
```

The JRE will allow you to run almost all Java software.

Verify the installation with:

```bash
java -version
```

You will receive the output similar to the following:

```text
openjdk version "17.0.9" 2023-10-17
OpenJDK Runtime Environment (build 17.0.9+9-Ubuntu-123.04)
OpenJDK 64-Bit Server VM (build 17.0.9+9-Ubuntu-123.04, mixed mode, sharing)
```

You may need the JDK in addition to the JRE in order to compile and run some specific Java-based software:

```bash
sudo apt install default-jdk
```

Verify the JDK with:

```bash
javac -version
```

You will see the following output:

```text
javac 17.0.9
```

## Step 2: Installing Scala

Install curl with the following command: 

```bash
sudo snap install curl  # version 8.1.2
```

Or

```bash
sudo apt  install curl  # version 7.88.1-8ubuntu2.3
```

To install Scala, it is recommended to use `cs setup` - the Scale installer powered by Coursier.

```bash
curl -fL https://github.com/coursier/coursier/releases/latest/download/cs-x86_64-pc-linux.gz | gzip -d > cs && chmod +x cs && ./cs setup
```

You may need to log out an dlog back in (or reboot) in order for the changes to take effect.

Check the setup with the command:

```bash
$ scala -version
Scala code runner version 3.4.2 -- Copyright 2002-2024, LAMP/EPFL
```

## Step 3: Installing Spark

Download Spark: [spark-3.5.1-bin-hadoop3.tgz](https://www.apache.org/dyn/closer.lua/spark/spark-3.5.1/spark-3.5.1-bin-hadoop3.tgz)

In Downloads directory, extract the Spark tar file:

```bash
tar xvf spark-3.5.1-bin-hadoop3.tgz
```

Move Spark files to respective directory (**/usr/local/spark**):

```bash
sudo mv spark-3.5.1-bin-hadoop3.tgz /usr/local/spark
```

Set up the environment for Spark:

```bash
export PATH=$PATH:/usr/local/spark/bin
```

Use the following command for sourcing the ~/.bashrc file:

```bash
source ~/.bashrc
```

Verify the Spark installation:

```bash
$ spark-shell
24/08/07 08:50:17 WARN Utils: Your hostname, quoct resolves to a loopback address: 127.0.1.1; using 192.168.17.131 instead (on interface ens33)
24/08/07 08:50:17 WARN Utils: Set SPARK_LOCAL_IP if you need to bind to another address
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
24/08/07 08:50:24 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Spark context Web UI available at http://192.168.17.131:4040
Spark context available as 'sc' (master = local[*], app id = local-1722995425361).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 3.5.1
      /_/
         
Using Scala version 2.12.18 (OpenJDK 64-Bit Server VM, Java 17.0.9)
Type in expressions to have them evaluated.
Type :help for more information.

scala> 
```