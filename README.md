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
1. First verify elasticsearch is up. On base machine hit http://{base machine Ip}:9200
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
3. Inside elk container edit logstash configuration file to take input from Filebeat, process input and forward to elasticsearch.
```
Edit logstash configuration file. Replace the contents of the file from logstash.conf file in this repository and save it.
$ sudo vi /etc/logstash/conf.d/logstash.conf

Start logstash deamon using below command
$ /opt/logstash/bin/logstash -f logstash.conf
```
4. Start your topology and start POX with opennetmon.
5. On base machine open browser and hit http://{base machine Ip}:5601/app/kibana . Kibana UI will be up. In Settings tab search your index. (In logstash.conf, you can set an index name, currently it is set to filebeat-{DATE}).
6. In discover tab you can see the logs from opennetmon is being fectched. In visualise and dashboard tab you can create graphs according to your needs.
