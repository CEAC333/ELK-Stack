# ELK-Stack

# Installation

- Detailed Instructions: 

http://sundog-education.com/elasticsearch/

### Installing VirtualBox
- https://www.virtualbox.org/wiki/Downloads

### Installing Ubuntu
- https://www.ubuntu.com/download/server

### Installing Elasticsearch

#### Once inside ubuntu with everything configured
```
sudo apt-get install default-jdk
```
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
```
sudo apt-get install apt-transport-https
```
```
echo "deb https://artifacts.elastic.co/packages/5.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-5.x.list
```
```
sudo apt-get update && sudo apt-get install elasticsearch
```
```
sudo nano /etc/elasticsearch/elasticsearch.yml
```
It'll open the file and you need to uncomment the line and change the ip:
```
#network.host: 192.168.0.1
```
And it should look like this:
```
network.host: 0.0.0.0
```
Write the changes and exit from nano; then continue with the following commands
```
sudo /bin/systemctl daemon-reload
```
```
sudo /bin/systemctl enable elasticsearch.service
```
```
sudo /bin/systemctl start elasticsearch.service
```
```
curl 127.0.0.1:9200
```
If everything is okay, you should see a response like this:
```
{
  "name" : "KISMR_n",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "sxn_nDnpQ6i3UHxvbNmmjQ",
  "version" : {
    "number" : "5.6.5",
    "build_hash" : "6a37571",
    "build_date" : "2017-12-04T07:50:10.466Z",
    "build_snapshot" : false,
    "lucene_version" : "6.6.1"
  },
  "tagline" : "You know, for Search"
}
```
# First Excercise
```
wget http://media.sundog-soft.com/es/shakes-mapping.json
```
```
curl -XPUT 127.0.0.1:9200/shakespeare --data-binary @shakes-mapping.json
```
```
wget http://media.sundog-soft.com/es/shakespeare.json
```
```
curl -XPOST 127.0.0.1:9200/shakespeare/_bulk --data-binary @shakespeare.json
```
```
curl -XGET '127.0.0.1:9200/shakespeare/_search?pretty' -d '
{
"query" : {
"match_phrase" : {
"text_entry" : "to be or not to be"
}
}
}
'
```

# Reference
https://www.udemy.com/elasticsearch-and-elastic-stack-in-depth-and-hands-on
