# elk-opennetmon
elk stack integration with opennetmon for network performance visualization. We are using Filebeat to forward the logs to logstash for processing.

#Setting up elk container
(original source : http://elk-docker.readthedocs.io/). The following commands are used:
```
$ sudo docker pull sebp/elk
$ sudo docker run -p 5601:5601 -p 9200:9200 -p 5000:5000 -it --name elk sebp/elk
```
Open ports description:
1. 5601 - Kibana web interface
2. 9200 - Elasticsearch JSON interface
3. 5000 - Logstash forwarder

#Running ELK stack
1. First verify elasticsearch is up. hit http://{base machine Ip}:9200
2. Install Filebeat on base machine and start the daemon
```
download and install filebeat
$ curl -L -O https://download.elastic.co/beats/filebeat/filebeat_1.1.0_amd64.deb
$ sudo dpkg -i filebeat_1.1.0_amd64.deb
Edit filebeat configuration file. Replace the contents of the file from filebeat.yml file in this repository and save it.
$ sudo vi /etc/filebeat/filebeat.yml
Start filebeat deamon using below command
$ /usr/bin/filebeat -e -c filebeat.yml -d "publish"
```
