# json-jsonp
Difference between JSON &amp; JSONP

 down vote
	

JSON

JSON (Javascript Object Notation) is a convenient way to transport data between applications, especially when the destination is a Javascript application.

Example :

Here is a minimal example that uses JSON as the transport for the server response. The client makes an ajax request with the JQuery shorthand function $.getJSON. The server generates a hash, formats it as JSON and returns this to the client. The client formats this and puts it in a page element.

Link : Difference between json & jsonp
```
Server:

get '/json' do
 content_type :json
 content = { :response  => 'Sent via JSON',
            :timestamp => Time.now,
            :random    => rand(10000) }
 content.to_json
end
```

```
Client:

var url = host_prefix + '/json';
$.getJSON(url, function(json){
  $("#json-response").html(JSON.stringify(json, null, 2));
});

```
```
Output:

  {
   "response": "Sent via JSON",
   "timestamp": "2014-06-18 09:49:01 +0000",
   "random": 6074
  }

```
JSONP (JSON with Padding)

JSONP is a simple way to overcome browser restrictions when sending JSON responses from different domains from the client. The only change on the Client side with JSONP is to add a callback parameter to the URL

```
Server:

get '/jsonp' do
 callback = params['callback']
 content_type :js
 content = { :response  => 'Sent via JSONP',
            :timestamp => Time.now,
            :random    => rand(10000) }
 "#{callback}(#{content.to_json})"
end
```
```
Client:

var url = host_prefix + '/jsonp?callback=?';
$.getJSON(url, function(jsonp){
  $("#jsonp-response").html(JSON.stringify(jsonp, null, 2));
});

```
```
Output:

 {
  "response": "Sent via JSONP",
  "timestamp": "2014-06-18 09:50:15 +0000",
  "random": 364
}
```
