vi /etc/logstash/conf.d/beats.conf

input {
    beats {
	port=> 5044
    }
}
filter {
   if [type] == "syslog" {
       grok {
	     match => { "message" => "% {SYSLOGLINE}"}
	}
	date {
	     match => [ "timestamp", "MMM d HH:mm:ss", MMM dd HH:mm:ss" ]
			       }	
		}	
}
output {
     elasticsearch {
	hosts => [ "54.237.58.24:9200"]
	index => "%{[@metadata][beat]}-%{+YYYY.MM.dd}"
		}
	}

# change the ownership and permision
chown -R logstash:logstash /etc/logstash/conf.d/beats.conf
chmod -R 755 /etc/logstash/conf.d/beats.conf
# start and enable the service
systemctl start logstash
systemctl enable logstash


yum -y install filebeat

# configure the filebeat

vi /etc/filebeat/filebeat.yml

----------- elasticsearch output-------------------
comment the below lines
#output.elasticsearch
#hosts

output.logstash:
	# the Logstash hosts
	hosts: ["54.237.58.24:5044"]

 -----------------------------filebeat inputs -----------------------

- /var/log/messages

systemctl start filebeat
systemctl enable filebeat



# after that start installing file beat in client machine 

install elastic search
install filebeat

vi /etc/filebeat/filebeat.yml

-------------------------elasticsearch output-----------------------
comment the line add logstatsh

comment the below lines
#output.elasticsearch
#hosts

output.logstash:
	# the Logstash hosts
	hosts: ["	:5044"]

give main elk ip address

filebeat modules list
filebeat modules enbale system    >> output module is enabled

vi /etc/filebeat/modules.d/system.yml

- module: system ## change *log to messages
	var.paths: ["var/log/messages"]


systemctl enable filebeat
systemctl start filebeat

management>> stack management>> index pattern 
