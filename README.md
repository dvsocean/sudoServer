    
1. To launch a standalone server run "java -jar wiremock-standalone-2.20.0.jar". 
This command will create two directories, "__files" and "mappings" (if they dont already exist).
When wiremock starts, by default it will spin up on port 8080 or you can specify a different 
port like this, "java -jar wiremock-standalone-2.20.0.jar --port \<port\>".

2. The __files directory serves as the root for files, in other words, if you place in it a file 
called randomFileDemonstration.html, once the server starts you can access it like you would any 
website, just open your browser and type http://localhost:/\<port\>/randomFileDemonstration.html

3. The mappings directory serves as the root for json files. You can place your req/res stubs in
it and it will serve them if the route matches. Currently, there is a stub called "stubWithBody.json"
and it contains the request and the response. You can make a curl request and test it. Or, in the 
mapping file, for the response, you can also indicate "bodyFileName": "path/to/file.json". Using this 
method requires that you actually place the response file in the __files directory, else if the 
route on the mapping stub is hit it will look for the corresponding body file and not find it, resulting 
in a error. You can also test this by sending a POST request to /test/server/route and include
a json body of '{"pin":"1234","securityQuestions":"and then answers"}' if needed, examples on sending 
a curl request can be found in the root, under "sendCurlRequestExample.txt"

4. You can also record a req/res with wiremock. For example, your in the middle of development and 
all your APIs are properly responding. You can capture this behavior for when and if these APIs decide
to misbehave. I recommend making a directory for the wiremock-standalone-2.20.0.jar since you will end
up using it for a few things. To record just execute 
"java -jar wiremock-standalone-2.20.0.jar --proxy-all http://url/to/your/service --record-mappings 
--port \<port\> --root-dir \<path/to/directory\>" from the directory where wiremock-standalone-2.20.0.jar
resides. Lets break this down. The --proxy-all flag tells wiremock to direct all (req and res) traffic
thru the indicated port. --record-mappings flag instructs wiremock to record the traffic. The other
flag I found handy is the --root-dir flag, this tells wiremock to store all the recorded mappings in a
particular directory. So say you have, 5 different services that could possibly send a response or receive 
a request..you can listen to all of them at once and for each service you can specify --root-dir
/User/\<user\>/Desktop/HttpTraffic/service1, --root-dir /User/\<user\>/Desktop/HttpTraffic/service2, 
--root-dir /User/\<user\>/Desktop/HttpTraffic/service3..etc. This will create one folder on your desktop 
called "HttpTraffic" and inside you will find a folder for each service (service1,service2,service3..etc). 
Inside each service folder you will find a __files and a mappings directory where the recorded stubs can 
be found. 

5. In the request, a stub will look for bodyPatterns, those patterns will usually be under "equalToJson". 
Your request could have a lot of different parameters but undersatnd that a match will occur when the 
specified parameters are found (with the specified values). At that point the response will be served. 
In this way, we can make a stub global. For example, anytime a request contains age of 25 ({"age":25}), 
serve up this response. Your actual request could contain age, address, id and so forth but since we are 
including age there will be a match. So any request that contains the age parameter will recieve the 
corresponding response. You can also remove the request body entirely, at this point only the endpoint 
needs to match for the response to be served. This is an overview, simply to give you an idea of how 
flexible wiremock is. For further information I recommend reading and learning directly from their website 
at http://wiremock.org . Happy developing!









