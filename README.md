# elk-opennetmon
elk stack integration with opennetmon for network performance visualization:

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
