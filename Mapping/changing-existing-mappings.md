# Changing existing mappings
#### mappings of existing fields cannot be changed, we have to delete the index and create mapping

## Deleting the index

```
DELETE /product
```

## Creating index with mappings

```
PUT /product
{
  "mappings": {
    "default": {
      "dynamic": false,
      "properties": {
        "in_stock": {
          "type": "integer"
        },
        "is_active": {
          "type": "boolean"
        },
        "price": {
          "type": "integer"
        },
        "sold": {
          "type": "long"
        }
      }
    }
  }
}
```

"default" is the type name
