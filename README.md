# logstash-configs

Most of the guidance for importing Wikipedia data originated from http://serverfault.com/questions/615196/logstash-parsing-xml-document-containing-multiple-log-entries.

The raw XML feed data will need sanitized so we can better instruct the Logstash multiline filter. `xmllint` is good for this.

```
cat wikimedia-data.xml | tr -d "\n\r" | xmllint --format -
```

Start Logstash with the configuration.

```
logstash -f logstash-wikimedia-xml.conf
```

Now paste data directly into the console. Be sure to include the enclosing `<doc></doc>` tags like this:

```
  <doc>
    <title>Wikipedia: Chengziya Ruins</title>
    <url>https://en.wikipedia.org/wiki/Chengziya_Ruins</url>
    <abstract>#REDIRECT Chengziya Archaeological Site</abstract>
    <links/>
  </doc>
  <doc>
    <title>Wikipedia: Emergency 4</title>
    <url>https://en.wikipedia.org/wiki/Emergency_4</url>
    <abstract>#REDIRECT Emergency 4: Global Fighters for Life</abstract>
    <links/>
  </doc>
  <doc>
  ```
  
Be sure to hit <enter> after the last entry or a parse error will result. Still working out the kinks to make it reliable. Pull requests welcome!
