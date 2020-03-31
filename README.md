# elk_ci

Filebeat is called "forwarder" , which forwards files from remote nodes
Elastic seracher is called "indexer"

And in between comes logstash




ELBK setup :
https://www.youtube.com/playlist?list=PLsgnv1SN76IJs44b2HNJYM_i64NzijlZx

Logstash:

Try:

1. logstash -e "input{stdin{}} output{stdout{}}
   Now enter any text and logstash will add some more content like version etc and print to std output
   
2.    


Filters :

1. CSV filter-tutorial-patterns

2. Mutate Filter

3. Grok Filter:

use the pre-canned grok pattern for Apache

%{COMBINEDAPACHELOG}

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
http://localhost:9200/_cat/indices


Kibana :
  It runs on Node Js
  
  
  
  
Docker :

docker pull logstash:7.6.1
docker run -it --rm logstash:7.6.1 --version
docker run -it --rm logstash:7.6.1 -e 'input { stdin { } } output { stdout { } }'
docker run -it --rm logstash:7.6.1 -e 'input { stdin { } } output { stdout { codec => rubydebug } }'

docker run -it --rm --name logstash --entrypoint bash logstash




docker pull elasticsearch:7.6.1


docker pull kibana:7.6.1

Part 1 : https://vocon-it.com/2016/11/17/logstash-hello-world/
Part 2 : https://vocon-it.com/2016/11/18/elasticsearch-hello-world-example/
Part 3 : https://vocon-it.com/2016/11/20/kibana-hello-world-example/

https://itnext.io/deploy-elk-stack-in-docker-to-monitor-containers-c647d7e2bfcd

  