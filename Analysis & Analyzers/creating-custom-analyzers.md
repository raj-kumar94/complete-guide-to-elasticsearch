# Creating custom analyzers

## Adding a custom analyzer

```
PUT /analyzers_test
{
  "settings": {
    "analysis": {
      "filter": {
        "my_stemmer": {
          "type": "stemmer",
          "name": "english"
        }
      },
      "analyzer": {
        "english_stop": {
          "type": "standard",
          "stopwords": "_english_"
        },
        "my_analyzer": {
          "type": "custom",
          "tokenizer": "standard",
          "char_filter": [
            "html_strip"
          ],
          "filter": [
            "standard",
            "lowercase",
            "trim",
            "my_stemmer"
          ]
        }
      }
    }
  }
}
```

## Testing the custom analyzer

```
POST /analyzers_test/_analyze
{
  "analyzer": "my_analyzer",
  "text": "I'm in the mood for drinking <strong>semi-dry</strong> red wine!"
}
```


# create an autocomplete analyser
<pre><code>
PUT blogs
{
  "settings": {
    "analysis": {
      "filter": {
        "autocomplete_filter": {
          "type":"edge_ngram",
          "min_gram":1,
          "max_gram":20
        }
      },
      "analyzer":{
        "autocomplete":{
          "type":"custom",
          "tokenizer":"standard",
          "filter":[
            "lowercase",
            "autocomplete_filter"
          ]
        }
      }
    }
  }
}
</code></pre>


> testing the analyzer:
<pre><code>
POST blogs2/_analyze
{
  "analyzer": "autocomplete",
  "text": "java"
}
</code></pre>





> now map your field with it
<pre><code>
PUT blogs/_mapping/post
{
  "post": {
    "properties":{
      "title":{
        "type":"text",
        "analyzer":"autocomplete"
      }
    }
  }
}
</code></pre>

> type -> text/string

> but only use n-grams on the index side, otherwise our query will also get split into n-grams and we will get results for everything that matches 'j', 'a', 'v', 'a', 'ja', 'av' etc.

<pre><code>
{
  "query": {
    "match":{
      "title":{
        "query":"java",
        "analyzer":"standard"
      }
    }
  }
}
</code></pre>
