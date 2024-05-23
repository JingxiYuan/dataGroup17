## Local Install and Test of ElasticSearch

https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

### Start a single-node cluster

Create network

```
docker network create elastic
```

Pull ElasticSearch docker image

```
docker pull docker.elastic.co/elasticsearch/elasticsearch:8.13.3
```

Start an ElasticSearch container

```
docker run --name esnode01 --net elastic -p 9200:9200 -it -m 1GB docker.elastic.co/elasticsearch/elasticsearch:8.13.3
```
Output below

```
ℹ️ Configure other nodes to join this cluster:
• Copy the following enrollment token and start new Elasticsearch nodes with `bin/elasticsearch --enrollment-token <token>` (valid for the next 30 minutes):
  eyJ2ZXIiOiI4LjEzLjMiLCJhZHIiOlsiMTcyLjE4LjAuMjo5MjAwIl0sImZnciI6ImViOTE5OThmNzE4NmI1ZmQ1ZDUwODY3MWI4NTZkZWU5NmNkMTYwMTNlZjA4ZjM2OWQ3N2ZkMWEzNWYyOGMxYjAiLCJrZXkiOiJWWkdDUG84QnRJakxjdGFmOHBORDpWbDh4MENOUFJmRy10VGRib2dJX3R3In0=

  If you're running in Docker, copy the enrollment token and run:
  `docker run -e "ENROLLMENT_TOKEN=<token>" docker.elastic.co/elasticsearch/elasticsearch:8.13.3`

```

Password and enrollment tokens are created when you start elastic search for the first time. Use the below commands to regenerate these

```
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
docker exec -it es01 /usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

Set environment variable

```
export ELASTIC_PASSWORD="your_password"
```