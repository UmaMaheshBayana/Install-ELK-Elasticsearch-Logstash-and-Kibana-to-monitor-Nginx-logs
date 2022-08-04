# Install ELK Elasticsearch Logstash and Kibana to monitor Nginx logs

# Step-1 : Steps to install ElasticSearch on Ubuntu 20.04 LTS

**Install Java  – OpenJDK on Ubuntu 20.04**

ElasticSearch needs Java installation for proper working and to install it on Ubuntu, we just need to use a single command. As Java is already in the official repository, thus run

```
sudo apt install default-jdk
````

***Check the Java version once the installation is completed***

```
java --version
````

***Add Elasticsearch GPG key***

To make sure the packages we will get from the Elasticsearch repository are from the genuine source and signed by the Public key generated for it, add Elasticsearch GPG key.

```
sudo apt-get install apt-transport-https
````

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
````
 
***As Ubuntu is a Debian-based Linux, hence we can add ElasticSearch’s official repository available to download Debian packages meant for it***

```
sudo sh -c 'echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" > /etc/apt/sources.list.d/elastic-7.x.list'
````
***Run system updateTo flush the repository cache and rebuild it again, so that the system could recognize the packages available to download in the newly added repository.***

```
sudo apt update
````
 
***Command to install Elasticsearch on Ubuntu 20.04 LTS***

Finally, here is the command to download the required packages to set up ElasticSearch on Ubuntu 20.04 LTS server or Desktop using the command terminal.

```
sudo apt install elasticsearch
````
***Configure Elasticsearch***
```
sudo nano /etc/elasticsearch/elasticsearch.yml
````
Here in this configuration file uncomment the lines mentioned   

```cluster.name: my-application```

```cluster.initial_master_nodes: ["node-1", "node-2"]```

And Change IP addres for network Host

```network.host: 0.0.0.0```

***Enable and Start Elasticsearch Service Once the installation is completed, let’s enable its service to start it automatically with system boot.***

```
sudo systemctl daemon-reload
````

```
sudo systemctl enable elasticsearch
````

***Command to Start Elasticsearch***

```
sudo systemctl start elasticsearch
````

***Command to Check Status*** 

```
sudo systemctl status elasticsearch
````

***Note– In the future to stop the same service you can use this:***

```
sudo systemctl stop elasticsearch
````
 
***Verify Elasticsearch is working properly***

Now everything is up and running on your system for ElasticSearch, it’s time to check whether it is working fine or not. So, to test it we use CURL.

```
sudo apt-get install curl
````

Now test the Elasticsearch by sending an HTTP request with port number 9200

```
curl -X GET "localhost:9200/"
```

To check Elasticsearch on chrome, Open chrome and type ```localhost:9200``` (here elastic server run on port 9200) 


***Uninstall (optional)***

In the future, if you want to remove ElasticSearch from your Ubuntu Linux then use the below command to do that:

```
sudo apt-get --purge autoremove elasticsearch
````

To completely remove it from the system also delete its directory if there is any using the below command:

```
sudo rm -rf /var/lib/elasticsearch/
````

```
sudo rm -rf /etc/elasticsearch
````

# Step 2: Install Kibana And Configure Elasticsearch

***After Elasticsearch install please follow the below setps to install and configure KIBANA***

***Command to install Kibana*** 

```
sudo apt install kibana
````
***Then enable and start the Kibana service***

```
sudo systemctl enable kibana
````
```
sudo systemctl start kibana
````

To check Kibana Status

```
sudo systemctl status kibana
````

***Configure Kibana and ElasticSearch***

To configure Elasticsearch to Kibana go to the below mentioned path to change ```kibana.yml``` file

```
sudo nano /etc/kibana/kibana.yml
````

Here uncomment the below mentioned lines to change configurations

```server.port: 5601```

```server.host: '0.0.0.0'```

```server.maxPayload: 1048576```

```elasticsearch.hosts: ['http://127.0.0.1:9200']```

```kibana.index: '.kibana'```

after changing the configaution save the ```kibana.yml``` file

***Now enable the kibana and Start Kibana***

```
sudo systemctl enable kibana
````
```
sudo systemctl start kibana
````
```
sudo systemctl status kibana
````
After start the kibana, Open chrome and type ```localhost:5601``` (here kibana server run on port 5601) 


