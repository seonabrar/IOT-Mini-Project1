<div align="center">
<h1 align="center">
<img src="https://raw.githubusercontent.com/PKief/vscode-material-icon-theme/ec559a9f6bfd399b82bb44393651661b08aaf7ba/icons/folder-markdown-open.svg" width="100" />
<br>FIT-LAB-MQTT-AWSIOT</h1>
<h3>◦ Developed with the software and tools below.</h3>
<h3>◦ ► FIT-IoT testbed, RIOT, AWS cloud, Mosquitto MQTT, NodeRed, Influxdb, Grafana</h3>
<p align="center">
<img src="https://img.shields.io/badge/C-A8B9CC.svg?style=for-the-badge&logo=C&logoColor=black" alt="C" />
<img src="https://img.shields.io/badge/JSON-000000.svg?style=for-the-badge&logo=JSON&logoColor=white" alt="JSON" />
</p>
<img src="https://img.shields.io/github/license/Awais-Mughal/FIT-LAB-MQTT-AWSIOT?style=for-the-badge&color=5D6D7E" alt="GitHub license" />
<img src="https://img.shields.io/github/last-commit/Awais-Mughal/FIT-LAB-MQTT-AWSIOT?style=for-the-badge&color=5D6D7E" alt="git-last-commit" />
<img src="https://img.shields.io/github/commit-activity/m/Awais-Mughal/FIT-LAB-MQTT-AWSIOT?style=for-the-badge&color=5D6D7E" alt="GitHub commit activity" />
<img src="https://img.shields.io/github/languages/top/Awais-Mughal/FIT-LAB-MQTT-AWSIOT?style=for-the-badge&color=5D6D7E" alt="GitHub top language" />
</div>

---

##  Table of Contents
- [ Table of Contents](#-table-of-contents)
- [ Overview](#-overview)
- [ repository Structure](#-repository-structure)
- [ Modules](#modules)
- [ Getting Started](#-getting-started)
    - [ Installation](#-installation)
    - [ Running FIT-LAB-MQTT-AWSIOT](#-running-FIT-LAB-MQTT-AWSIOT)
    - [ Tests](#-tests)
    - [ Dashboard](#-dashboard)



---


##  Overview

 In this project an IoT (Internet of Things) sensor node is developed using the RIOT operating system. The sensor node is designed to collect environmental data, including temperature and pressure, and transmit this data to an MQTT (Message Queuing Telemetry Transport) broker using secure protocols,The sensor node communicates with an MQTT broker, and the Mosquitto broker bridge is configured to connect to AWS IoT. and visualizes the data through Grafana.

![Alt text](/images/image17.png)

---


##  Repository Structure

```sh
└── FIT-LAB-MQTT-AWSIOT/
    ├── Broker_config/
    │   └── config.conf
    ├── Grafana/
    │   └── Grafana_Dashboard.json
    ├── Mosquitto_Bridge/
    │   └── mosquitto.config
    ├── NodeRed/
    │   └── NodeRed_Flow.json
    └── Sensor_node/
        ├── Makefile.mak
        └── main.c

```

---


##  Modules

<details closed><summary>Broker_config</summary>

| File                                                                                                   | Summary       |
| ---                                                                                                    | ---           |
| [config.conf](https://github.com/Awais-Mughal/FIT-LAB-MQTT-AWSIOT/blob/main/Broker_config/config.conf) | ► The config.conf file enables MQTT-SN and MQTT connections, with debug tracing and specific listeners. It also establishes a connection named "local_bridge_to_ec2" between local and AWS IoT gateways on respective ports.|

</details>

<details closed><summary>Sensor_node</summary>

| File                                                                                                   | Summary       |
| ---                                                                                                    | ---           |
| [main.c](https://github.com/Awais-Mughal/FIT-LAB-MQTT-AWSIOT/blob/main/Sensor_node/main.c)             | ► The C program for the IoT sensor node, named "SensorNode," includes MQTT-SN communication, LPS331AP sensor readings, and a command-line interface (CLI). It periodically measures temperature and pressure, publishes the data to an MQTT broker, and provides status reports via the CLI. The program creates threads for MQTT communication and the main measurement loop. |
| [Makefile.mak](https://github.com/Awais-Mughal/FIT-LAB-MQTT-AWSIOT/blob/main/Sensor_node/Makefile.mak) | ► The Makefile for the SensorNode application in RIOT OS configures a native board, includes necessary modules for sensor and network functionality, sets up MQTT modules for communication, and defines parameters such as server address, port, and MQTT topics.|

</details>

<details closed><summary>Grafana</summary>

| File                                                                                                                   | Summary       |
| ---                                                                                                                    | ---           |
| [Grafana_Dashboard.json](https://github.com/Awais-Mughal/FIT-LAB-MQTT-AWSIOT/blob/main/Grafana/Grafana_Dashboard.json) | ► It includes panels displaying temperature and pressure information over time, with thresholds for visualization. The dashboard is designed to refresh every 5 seconds.|

</details>

<details closed><summary>Nodered</summary>

| File                                                                                                         | Summary       |
| ---                                                                                                          | ---           |
| [NodeRed_Flow.json](https://github.com/Awais-Mughal/FIT-LAB-MQTT-AWSIOT/blob/main/NodeRed/NodeRed_Flow.json) | ► The Node-RED flow titled "Flow 1" includes MQTT input for the topic "localgateway_to_awsiot," with subsequent debugging and storage in InfluxDB. It warns about container setup for preserving flow changes in Docker. The MQTT input connects to the broker at 52.204.227.162:1883, and InfluxDB storage uses the database "iot" at 127.0.0.1:8086.|

</details>

<details closed><summary>Mosquitto_bridge</summary>

| File                                                                                                                | Summary       |
| ---                                                                                                                 | ---           |
| [mosquitto.config](https://github.com/Awais-Mughal/FIT-LAB-MQTT-AWSIOT/blob/main/Mosquitto_Bridge/mosquitto.config) | ► It sets up an MQTT bridge to AWS IoT Core. It includes connection details such as the AWS IoT ATS endpoint, specifies bridged topics for bidirectional communication, sets the MQTT protocol version, enables SSL/TLS with certificate-based authentication, and configures cleanup and logging options. |

</details>

---

##  Getting Started

###  Installation

1. Clone the FIT-LAB-MQTT-AWSIOT repository:
```sh
git clone https://github.com/Awais-Mughal/FIT-LAB-MQTT-AWSIOT
```

2. Change to the project directory:
```sh
cd FIT-LAB-MQTT-AWSIOT
```

###  Running FIT-LAB-MQTT-AWSIOT

1. Connect to Grenoble SSH Frontend
```bash
ssh <login>@grenoble.iot-lab.info
```

2. Start Experiment on IoT-Lab Test Bed

Launch an experiment with two M3 nodes and one A8 node
Wait for the experiment to reach the "Running" state
Get the list of nodes

3. Build Border Router Firmware
Source RIOT environment
```sh
source /opt/riot.source
```
Build border router firmware for M3 node with baudrate 500000
Note: Use a different 802.15.4 channel if needed
```sh
make ETHOS_BAUDRATE=500000 DEFAULT_CHANNEL=<channel> BOARD=iotlab-m3 -C examples/gnrc_border_router clean all
```


4. Flash Border Router Firmware
Flash the border router firmware to the first M3 node (m3-1 in this case)
```sh
iotlab-node --flash examples/gnrc_border_router/bin/iotlab-m3/gnrc_border_router.elf -l grenoble,m3,<node-id>
```


5. Configure Border Router Network
Choose an IPv6 prefix for the site (e.g., 2001:660:5307:3100::/64)
Configure the network of the border router on m3-<node-id>
Propagate an IPv6 prefix with ethos_uhcpd.py
```sh
sudo ethos_uhcpd.py m3-<node-id> tap0 2001:660:5307:3100::1/64
```

6. Setup MQTT Broker and Mosquitto Bridge on A8 Node
Now, in another terminal, SSH to the SSH frontend, and login into clone the mqtt_broker and mosquitto bridge configuration files in A8 shared directory.
SSH into the A8 node
```sh
ssh root@node-a8-1
```
Check the global IPv6 address of the A8 node
```sh
ifconfig
```
![Alt text](/images/image1.png)

7. Start MQTT Broker
From the A8 shared directory, start the MQTT broker using config.conf
```sh
cd ~/A8
broker_mqtts config.conf
```
![Alt text](/images/image2.png)

Configure and Start Mosquitto Bridge
From another terminal on the A8 node, check for existing mosquitto service and stop it
![Alt text](/images/image3.png)
Modify mosquitto.config with the IPv6 address of the Mosquitto broker (e.g., AWS-EC2 instance)

![Alt text](/images/image4.png)

Start Mosquitto service using the modified configuration file
```sh
root@node-a8-3:~/A8/mqtt_bridge# mosquitto -c mosquitto.conf
```

###  Tests
#### Build and Flash Sensor Node Firmware
From another terminal log into SSH front end of grenoble site
Clone the sensor node directory containing Makefile and main.c
Build the firmware for the sensor node using A8 node's IPv6 address and tap-id
```sh
make DEFAULT_CHANNEL=15 SERVER_ADDR=<IPv6 address> EMCUTE_ID=station(tap-id) BOARD=iotlab-m3 -C . clean all
```

#### Flash the sensor node firmware on an M3 node
```sh
iotlab-node --flash ./bin/iotlab-m3/SensorNode.elf -l grenoble,m3,<node-id>
```


#### Connect to Sensor Node
Log into the M3 node
```sh
nc m3-<node-id> 20000
```
![Alt text](/images/image5.png)

###  Dashboard 

1. Create EC2 instance and assign IPv6 subnet to the instance following tutorial : 
https://aws.amazon.com/blogs/networking-and-content-delivery/introducing-ipv6-only-subnets-and-ec2-instances/

2. Login to EC2 instance using SSH and install mosquitto broker:
```sh
sudo apt-add-repository ppa:mosquitto-dev/mosquitto-ppa
sudo apt-get update
sudo apt-get install mosquitto
sudo apt-get install mosquitto-clients
sudo apt clean
```
3. Verify if the mosquitto service is running:

```sh
sudo service mosquitto status
```
![Alt text](/images/image6.png)

4. Install docker engine on EC2 instance following the tutorial: https://docs.docker.com/engine/install/ubuntu/

5. Run the node NodeRed container on EC2 instance:

```sh
docker run -it -p 1880:1880 -v node_red_data:/data --name mynodered nodered/node-red
```
6. Run the node Influxdb container on EC2 instance:

```sh
docker run --detach --name influxdb -p 8086:8086 influxdb:2.2.0
```
7. Run the node Grafana container on EC2 instance:

```sh
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```
8. Allow public access on following ports in network security settings:

```sh
Port 1883 (default port for Mosquitto)
Port 1880 (default port for NodeRed)
Port 8086 (default port for Influxdb)
Port 3000 (default port for Grafana)
```
9. On influxdb, setup an organization name, for this project and create a bucket to collect data.

10. On node red add mqtt in network block and connect it to influx out storage block.

![Alt text](/images/image7.png)

11. Configure mqqt broker with the ip address and port of mosquitto broker running on EC2 instance.

![Alt text](/images/image8.png)

![Alt text](/images/image9.png)

12. Configure Influxdb out storage block with the ip address and port of influxdb service runnning on EC2 instances, and add details of bucket created in step 9.

![Alt text](/images/image10.png)
![Alt text](/images/image11.png)

13. On Grafana add influxdb as data sources, and add details for the influxdb bucket created in step 9.

![Alt text](/images/image12.png)
![Alt text](/images/image13.png)

14. Copy Query code from the influxdb bucket, and use it in grafana dashboard, to add visualization panel for each variable.
![Alt text](/images/image14.png)
![Alt text](/images/image15.png)

15. After repeating the previous step for each variable save the dashboard.
![Alt text](/images/image16.png)


###  Demo Video

[Demo Video](https://youtu.be/lsvIGaYIWuI)


