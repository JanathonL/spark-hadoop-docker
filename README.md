# Intro
A docker image for running spark on hadoop cluster with yarn cluster manager 
and HDFS.
> This develop branch only has 1 master node. The user machines can be added to the cluster one by one later.

# Note
* Make sure that you have installed the latest version of Docker.
* Make sure you have set enough memory space for Docker Engine. You can click the Docker symbol and select `Preferences/Advanced`. Then set the memory to a larger value depending on your laptop's memory size, and then click `Apply & Restart`.

# Run containers
The docker-compose.yml brings up one master and two slaves containers.<br />
To bring it up, simply use command `docker-compose up`

# To build an image only without bringing up containers
Use command "build.sh"

# Run MNIST sample training
Before running, run `cd sample && download.sh` to download the mnist dataset <br />
in host machine.

### Run with data and code at local machine
1. Connect to master docker node
2. `cd /sample`
3. `./mnist_data_convert.sh`
4. `./mnist_train.sh`
5. `./mnist_test.sh`

### Run with data and code at HDFS
1. Connect to master docker node
2. `cd /sample`
3. `hdfs_copy.sh`
3. `./hdfs_mnist_data_convert.sh`
4. `./hdfs_mnist_train.sh`
5. `./hdfs_mnist_test.sh`

After the test, you could find the result in hdfs under /user/root/predictions.<br />
When the task is running, you can connect to http://localhost:8088 to check the log. When you check the logs of each slave node, the Hadoop/Spark UI will redirect you to a URL with prefix slave1:8042 and slave2:8042. Simply modify them to localhost:8043 and localhost:8044, and you can then see the logs for each slave node.
