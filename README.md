# elk_ci

Demo environment of Kibana is available at 
https://demo.elastic.co/app/kibana


ELK stack has OSS,basic ,Gold,platinum and Enterprise liscensing system.

https://www.elastic.co/subscriptions


Choose liscensing carefully:
https://stackoverflow.com/questions/54079501/running-elastic-without-the-trial-license

Filebeat is called "forwarder" , which forwards files from remote nodes
Elastic seracher is called "indexer"

And in between comes logstash

Very good Docker setup 
https://medium.com/analytics-vidhya/elk-stack-in-docker-6285ec1ac1aa


ELBK setup :
https://www.youtube.com/playlist?list=PLsgnv1SN76IJs44b2HNJYM_i64NzijlZx

Common configurations to look into while setting up ELK :
https://cloudaffaire.com/how-to-install-and-configure-elasticsearch-cluster-in-linux/

Very nice list of articles for Elk
https://medium.com/elasticsearch/contents-cebdc419c8c9

Understanding Query
https://medium.com/@User3141592/understanding-the-elasticsearch-query-dsl-ce1d67f1aa5b 


Logstash:

Try:

1. logstash -e "input{stdin{}} output{stdout{}}"
   Now enter any text and logstash will add some more content like version etc and print to std output
   
2. logstash -f test.conf --config.test_and_exit 
    For testing if configuration is OK


Filters :

1. File based filter
  - CSV 
  - json
  - XML


2. Mutate Filter : it performs general mutations on fields. You can rename, remove, replace, and modify fields in your events.

3. Grok Filter:

use the pre-canned grok pattern for Apache

%{COMBINEDAPACHELOG}


4. ID based filters
   - UUID : it generate a string that’s unique for every event, even if the same input is processed multiple times.
   - fingerprint: Create consistent hashes (fingerprints) of one or more fields and store the result in a new field. This can e.g. be used to create consistent document ids when inserting events into Elasticsearch, allowing events in Logstash to cause existing documents to be updated rather than new documents to be created.

5. Date : The date filter is used for parsing dates from fields, and then using that date or timestamp as the logstash's default timestamp for that event.However another add_field cand be added to use the timestamp for someother purpose.

6. GeoIP: The GeoIP filter adds information about the geographical location of IP addresses, based on data from the Maxmind GeoLite2 databases.

7. Drop : Drops everything that gets to this filter.This is best used in combination with conditionals, for example following will cause all events matching to be dropped.
```
    filter {
      if [loglevel] == "debug" {
        drop { }
      }
    }
```
8. prune : The prune filter is for removing fields from events based on whitelists or blacklist of field names or their values (names and values can also be regular expressions).
           NOTE: This filter currently only support operations on top-level fields, i.e. whitelisting and blacklisting of subfields based on name or value does not work.

5. Ruby: Execute ruby code.


Note : Common Options are supported by all filter plugins:
- add_field
- add_tag
- enable_metric
- id
- periodic_flush
- remove_field
- remove_tag

https://qbox.io/blog/logstash-grok-filter-tutorial-patterns

https://logz.io/blog/logstash-grok/


Introduction to the Logstash Grok
https://www.youtube.com/watch?v=ReZLppwvBGM

 Logstash Filter using GROK plugin -1
https://www.youtube.com/watch?v=FZeN_wIh_pM

 Logstash Filter using GROK plugin -2
https://www.youtube.com/watch?v=TZoyfkZ6PdQ


Online editor

https://grokdebug.herokuapp.com/

List of grok patterns :

https://github.com/logstash-plugins/logstash-patterns-core/blob/master/patterns/grok-patterns

4. Geoip Filter:

5. userAgent Filter :





Elastic Search:

Elasticsearch from the bottom up
https://www.youtube.com/watch?v=PpX7J-G2PEo

ElasticSearch in action
https://www.youtube.com/watch?v=oPObRc8tHgQ

Elasticsearch in an Hour
https://www.youtube.com/watch?v=UPkqFvjN-yI

Elasticsearch Do's, Don'ts and Pro-Tips
https://www.youtube.com/watch?v=c9O5_a50aOQ

Index 				--> Database
Type/mapping  		--> Table
Document 			--> Row

Create Explicit Schema for managing schema

List all index
http://localhost:9200/_cat/indices?v

&ts=0

https://www.elastic.co/guide/en/elasticsearch/reference/current/cat.html

?pretty=true --> formatted output 


Getting Down and Dirty with ElasticSearch by Clinton Gormley
https://www.youtube.com/watch?v=7FLXjgB0PQI


# Kibana :
  It runs on Node Js
  
  
Dashboard banner :
1. Create .png files and keep them at <kibana_installation_home_path>/src/legacy/ui/public/assets/favicons
2. Go to Markdown Visualization and use follwing code 
     ![Image](http://kibana_IP:5601/ui/favicons/setup.png)

  
  
  
# Kibna Visualization using Vega:

Intro : https://www.youtube.com/watch?v=lQGCipY3th8
Tutorial : 
       
      1. https://www.youtube.com/playlist?list=PLqhRANpamh63oDk0FHWTFbjQJfdFbg8vx
	  2. https://www.youtube.com/watch?v=4xAO01xCBpQ
	  3. https://www.youtube.com/watch?v=RDe7KOb_SLQ

https://vega.github.io/polestar/

https://vega.github.io/editor  


https://github.com/nyurik/kibana-vega-vis
  
Docker :
```
docker pull logstash:7.6.1
docker run -it --rm logstash:7.6.1 --version
docker run -it --rm logstash:7.6.1 -e 'input { stdin { } } output { stdout { } }'
docker run -it --rm logstash:7.6.1 -e 'input { stdin { } } output { stdout { codec => rubydebug } }'

docker run -it --rm --name logstash --entrypoint bash -e "xpack.security.enabled=false" logstash:7.6.1
```


```
docker pull elasticsearch:7.6.1

```

```
docker pull kibana:7.6.1
```
Part 1 : https://vocon-it.com/2016/11/17/logstash-hello-world/
Part 2 : https://vocon-it.com/2016/11/18/elasticsearch-hello-world-example/
Part 3 : https://vocon-it.com/2016/11/20/kibana-hello-world-example/

https://itnext.io/deploy-elk-stack-in-docker-to-monitor-containers-c647d7e2bfcd

  
  
Sample project 
https://webkid.io/blog/visualize-datasets-with-elk/  