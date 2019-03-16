    
1. To launch a standalone server run "java -jar wiremock-standalone-2.20.0.jar". 
This command will create two directories, "__files" and "mappings" (if they dont already exist).
When wiremock starts, by default it will spin up on port 8080 or you can specify a different 
port like this, "java -jar wiremock-standalone-2.20.0.jar --port <port>".

2. The __files directory serves as the root for files, in other words, if you place in it a file 
called randomFileDemonstration.html, once the server starts you can access it like you would any 
website, just open your browser and type http://localhost:<port>/randomFileDemonstration.html

3. The mappings directory serves as the root for json files. You can place your req/res stubs in
it and it will server them if the route matches. Currently, there is a stub called "stubWithBody.json"
and it contains the request and the response. You can make a curl request and test it. Or, in the 
mapping file, for the response, you can also indicate "bodyFileName": "path/to/file.json". Using this 
method requires that you actually place the response file in the __files directory, else if the 
route on the mapping stub is hit it will look for the corresponding body file and not find it, resulting 
in a error. You can also test this by sending a POST request to /test/server/route and include
a json body of '{"pin":"1234","securityQuestions":"and then answers"}' if needed, examples on sending 
a curl request can be found in the root, under "sendCurlRequestExample.txt"

4. 



