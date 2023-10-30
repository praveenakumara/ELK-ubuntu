# ELK-ubuntu

# Ubuntu Server with 22.04 LTS
# Java 8 or higher version
# 2 CPU and 4 GB RAM

sudo apt update

sudo apt install apt-transport-https

# 1:Install Java on Ubuntu 22.04 LTS

sudo apt install openjdk-11-jdk

java -version
# set java env variable

sudo nano /etc/environment

JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"

source /etc/environment

echo $JAVA_HOME

#  Install Elastic Stack

wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list

sudo apt-get update

sudo apt-get install elasticsearch

# Start elacticsearch services

sudo systemctl start elasticsearch

# Enable elacticsearch at system startup

sudo systemctl enable elasticsearch

# To check the status of elasticsearch

sudo systemctl status elasticsearch

# 3. Configure Elasticsearch ################################

sudo nano /etc/elasticsearch/elasticsearch.yml

# Go to Network section and uncomment (network.host:0.0.0.0) and replace your system IP with

# network.host: 0.0.0.0 And you need to add this line discovery.seed_hosts: [ ] in discovery section 

# second step is go to the BEGIN SECURITY AUTO CONFIGURATION and here you need to replace this true with false as shown in below:

xpack.security.enabled: false

sudo systemctl restart elasticsearch

# 4:Testing Elasticsearch

curl -X GET "localhost:9200" or http://systemIP:9200

# Uninstalling Elasticsearch

sudo apt-get --purge autoremove elasticsearch

sudo apt-get remove --purge elasticsearch

sudo rm -rf /etc/elasticsearch

# 5:Install Logstash

# Install Logstash using following command:

sudo apt-get install logstash

# Start the Logstash service:

sudo systemctl start logstash

# Enable the Logstash service:

sudo systemctl enable logstash

# To check the status of the service, run the following command:

sudo systemctl status logstash

# 6:Configure logstash on Ubuntu 22.04 LTS

sudo nano /etc/logstash/logstash.yml

# 7:Install Kibana

# Run the following command to install Kibana:

sudo apt-get install kibana

# Start the Kibana service:

sudo systemctl start kibana

# Enable the Kibana service:

sudo systemctl enable kibana

# Let’s check the status of kibana:

sudo systemctl status kibana

# 8:Configure Kibana on Ubuntu 22.04 LTS
open the kibana.yml configuration file for editing:

sudo nano /etc/kibana/kibana.yml
Uncomment this below lines and localhost replace with 0.0.0.0 (means any ip_address):

server.port: 5601
server.host: "localhost"
elasticsearch.hosts: ["http://localhost:9200"]

# After changing configuration file you need to restart kibana

sudo systemctl restart kibana

# 9:Accessing Kibana

http://ip_address:5601
