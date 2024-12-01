# Elastic Commands

#### Search all available data

`GET` \_search

#### Stats of nodes

`GET` \_cat/nodes?v

#### Stats of indices

`GET` \_cat/indices?v

#### Cluster health monitoring

`GET` \_cluster/health

#### Shards up and running

`GET` \_cat/shards?v

#### Create a new index as student

`PUT` \_student

#### Delete student index

`DELETE` \_student

#### Configure the student index

`PUT` \_student

```json
{
    "settings": {
        "number_of_shards": 2,
        "number_of_replicas": 2
    }
}
```
