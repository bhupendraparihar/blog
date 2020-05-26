---
title: Web Scraping through YQL and nodejs
date: 2020-05-22 12:33:17
tags:
---

Web scraping (web harvesting or web data extraction) is a computer software technique of extracting information from websites.

I used a node module call YQL(Yahoo Query Language) to achieve it. You may have many other ways to do the same.

1. npm install yql  (this will download yql module for your node project)

2. app.js file.

<pre>
var http = require("http");
var YQL = require("yql");
var port = 3000;
var serverUrl = "localhost";
var word = {
    "english": "",
    "hindi": ""
};


new YQL.exec('select * from data.html.cssselect where url="http://shabdkosh.com/" and css="p.engwotd"', function(response) {
    word.english = response.query.results.results.p.content;
});

new YQL.exec('select * from data.html.cssselect where url="http://shabdkosh.com/" and css=".indwotd"', function(response) {
    word.hindi = response.query.results.results.p.content;
});

var server = http.createServer(function(req, res) {
    console.log(word.english, word.hindi);
    res.setHeader('Content-Type', 'application/json');
    res.end(JSON.stringify(word));
});

console.log("Listening at " + serverUrl + ":" + port);
server.listen(port, serverUrl);
</pre>
3. node app.js

4. hit your url : http://localhost:3000/