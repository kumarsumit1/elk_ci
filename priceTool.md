india corona
https://stackoverflow.com/questions/51537063/url-format-for-google-news-rss-feed
https://news.google.com/rss/search?q="india corona"+when:7d
https://news.google.com/search?q=india%20corona&hl=en-IN&gl=IN&ceid=IN%3Aen


curl -X GET https://news.google.com/rss/search?q=india+corona
https://medium.com/datadriveninvestor/preventing-duplicate-data-for-elasticsearch-562b06e4c084

https://alexmarquardt.com/2018/07/23/deduplicating-documents-in-elasticsearch/



input {
  http_poller {
    urls => {
      url => "https://api.rss2json.com/v1/api.json?rss_url=https%3A%2F%2Fnews.google.com%2Frss%2Fsearch%3Fq%3Dindia%2Bcorona"
    }
    request_timeout => 60
    schedule => { every => "1m"}
	codec => "json"
    metadata_target => "http_poller_metadata"
  }
}

filter {
json { source => "message" }
split { field => "items" }


mutate {
        add_field => {
            "items_title" => "%{[items][title]}"
			"items_link" => "%{[items][link]}"
			"items_pubDate" => "%{[items][pubDate]}"
        }
    }


 prune {
        whitelist_names => [
            "^items\_"
        ]
    }
	
date {
		match => [ "items_pubDate" , "yyyy-MM-dd HH:mm:ss" ]
		
	}

fingerprint {
	source => ["items_link" , "items_title"]
	concatenate_sources => true
	target => "fingerprint"
	method => "SHA1"
	key => "1234ABCD"
	base64encode => true
	}

}


output {

   stdout { codec => rubydebug }
}

stdout { codec => dots }


elasticsearch {hosts => [ “http://your.elastic.domain.here" ]index => “borrow-history-write”document_type => “_doc”document_id => “%{fingerprint}”}