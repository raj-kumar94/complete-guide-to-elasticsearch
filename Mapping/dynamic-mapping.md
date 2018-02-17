# Dynamic mapping
similar to schema in sql databases
## Retrieving mapping

```
GET /product/default/_mapping
```

<code>
  {
  "product": {
    "mappings": {
      "default": {
        "properties": {
          "created": {
            "type": "date",
            "format": "yyyy/MM/dd HH:mm:ss||yyyy/MM/dd||epoch_millis"
          },
          "description": {
            "type": "text",
            "fields": {
              "keyword": {
                "type": "keyword",
                "ignore_above": 256
              }
            }
          },
          "in_stock": {
            "type": "long"
          },
          "instructor": {
            "properties": {
              "firstName": {
                "type": "text",
                "fields": {
                  "keyword": {
                    "type": "keyword",
                    "ignore_above": 256
                  }
                }
              },
              "lastName": {
                "type": "text",
                "fields": {
                  "keyword": {
                    "type": "keyword",
                    "ignore_above": 256
                  }
                }
              }
            }
          },
          "is_active": {
            "type": "boolean"
          },
          "match": {
            "properties": {
              "query": {
                "properties": {
                  "name": {
                    "type": "text",
                    "fields": {
                      "keyword": {
                        "type": "keyword",
                        "ignore_above": 256
                      }
                    }
                  }
                }
              }
            }
          },
          "name": {
            "type": "text",
            "fields": {
              "keyword": {
                "type": "keyword",
                "ignore_above": 256
              }
            }
          },
          "new_price": {
            "type": "long"
          },
          "price": {
            "type": "long"
          },
          "sold": {
            "type": "long"
          },
          "tags": {
            "type": "text",
            "fields": {
              "keyword": {
                "type": "keyword",
                "ignore_above": 256
              }
            }
          }
        }
      }
    }
  }
}
</code>

> for description there are multiple types-> "text" and "keyword"
