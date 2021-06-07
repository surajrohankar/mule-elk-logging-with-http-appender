HTTP Appender::

Logstash -> Elasticsearch -> Kibana


1) create account on elk cloud (https://www.elastic.co/)
2) select observability for logs -> scroll down, it asks to select cloud on which you want to maintain all these stuffs (aws, azure, google) 
  -> click on create deployment -> It will show you a popup window with username and password. You can simply copy and paste it somewhere 
     or you can download the file
3) close the popup
4) you will see "Open Kiban" option (sometime it asks to download kibana)
5) Scroll down -> you will have Easticsearch endpoint, Kibana endpoint and CloudId. Copy and paste these thing somewhere.
6) goto email and verify email
7) click on menu -> management -> stack management -> data -> index management -> index templates -> create template
8) click on menu -> management -> stack management -> kibana -> index pattern -> create index pattern -> 
  search for create template(created in 7th step) -> choose timestamp field
9) click on kibana discover -> select your index pattern

Mule Log4j configuration:

```
 <Appenders>
 	<Http name="ELK-Cloud" url="https://observability-deployment-d7446a.es.us-east-1.aws.found.io:9243/applogs/_doc">
		<Property name="Authorization" value="Basic ${authorization}" />
		<Property name="Content-Type" value="application/json" />
		<PatternLayout pattern='%msg' />
	</Http>
 </Appenders>
```

 url : elasticsearch ELK cloud url.
 
 /applogs : index name (refer 7th and 8th step).
 
 /_doc : api endpoint.
 
 authorization : base64 encoded form of username:password (refer step 2). this is not elk cloud login creds.
