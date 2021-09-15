# mongodb-elasticsearch-playground

## Usage

### Setup

```sh
docker compose up
docker compose exec mongo-0 mongo /docker-entrypoint-initdb.d/init.js
dcexec mongo-0 mongo --eval "rs.status();"
docker compose restart mongo-express
```

### Add data in mongo-express

Open http://localhost:8081/ and add some data.

### Elastic Search

```sh
curl -X POST -H 'Content-Type: application/json' "http://localhost:9200/_search" -d' { "query": { "match_all": {} } }' | jq
```

```json
{
  "took": 1,
  "timed_out": false,
  "_shards": {
    "total": 1,
    "successful": 1,
    "skipped": 0,
    "failed": 0
  },
  "hits": {
    "total": {
      "value": 1,
      "relation": "eq"
    },
    "max_score": 1,
    "hits": [
      {
        "_index": "test-database.test-collection",
        "_type": "_doc",
        "_id": "6141a787ec72917d6ced60ec",
        "_score": 1,
        "_source": {
          "contents": "can this be searched?",
          "title": "sample title"
        }
      }
    ]
  }
}
```
