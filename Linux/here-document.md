---
layout: docs
title: Here Document
permalink: /linux/here-document/
---

* toc
{: toc }

## Summary

Here Document 是在Linux Shell 中的一种特殊的重定向方式，它的基本的形式如下

~~~shell
cmd << delimiter
  Here Document Content
delimiter
~~~

## Example 1

~~~shell
fish@mangos:~$ cat << EOF
> First Line
> Second Line
> Third Line EOF
> EOF
First Line
Second Line
Third Line EOF
~~~

## Example 2

~~~shell
VIN="LIWNS38904NK89010"

cat > ./searchRelationshipHistory.json << EOF
{

  "attributes":["source","target","type","startTime","endTime","changeAt"],
  "filter": "target eq \"$VIN\"",
  "schemas": ["urn:ietf:params:scim:api:messages:2.0:SearchRequest"]
}

EOF

cat searchRelationshipHistory.json
~~~

## Fix redirection Permission denied

~~~bash
sudo bash -c 'cat > /usr/local/gitbucket/bin/start.sh << EOF
java -jar gitbucket.war --port=8082 --temp_dir=/data/webapps/gitbucket --gitbucket.home=/data/storages/gitbucket --max_file_size=1024

EOF'
~~~
