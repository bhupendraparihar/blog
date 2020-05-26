---
title: How to create blog using HEXO
date: 2019-05-08 21:13:40
tags:
---
### installing hexo cli 
```
$ npm install -g hexo-cli
```
### create hexo blog
```
$ hexo init <foldername>
```

### running the server
```
$ cd blog
$ npm install
$ hexo server
```
This will start a server at http://localhost:4000

## create a new post
```
$ hexo new "Post Title"
```
This will create a markdown(.md) file in source/_posts folder. Write your content in this markdown file to show on your blog home page

## create new page
```
$ hexo new page "page title"
```
This will createa new folder with page title name and then a index.md file into that folder