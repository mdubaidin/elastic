# CRUD Operations

#### Add new document in student index

`POST` student/\_doc

```json
{
    "name": "Mohd Ubaid Khan",
    "designation": "Software Developer",
    "qualifications": "BCA"
}
```

#### Add new document with custom ID

`POST` student/\_doc/18

```json
{
    "name": "Virat Kohli",
    "designation": "Indian Cricketer",
    "qualification": "11th Pass"
}
```

#### Delete a specific document by its ID

`DELETE` student/\_doc/<doc_id>

#### Get all documents

`GET` student/\_search

```json
{
    "query": {
        "match_all": {}
    }
}
```

#### Update existing document

`POST` student/\_update/<doc_id>

```json
{
    "doc": {
        "qualification": "BCA Pass",
        "age": 23
    }
}
```

#### Script based update

`POST` student/\_update/<doc_id>

```json
{
    "script": {
        "source": "ctx._source.age = params.new_age", // ctx means current doc
        "params": {
            "new_age": 25
        }
    }
}
```

#### Multi-line script

```json
{
    "script": {
        "source": """
        if (ctx._source.age <= 0) {
            ctx.op = 'delete'
        } else {
            ctx._source.age = 18
        }
        """
    }
    // ctx.op means the operation to be performed. Here is a delete operation execute if age is less than or equal to 0
}
```

#### Update and Upsert

`POST` student/\_update/17

```json
{
    "script": {
        "source": "ctx._source.age = 18"
    },
    "upsert": {
        "name": "AB De Villiers",
        "designation": "South African Cricketer",
        "qualification": "N/A",
        "age": 40
    }
}
```

#### Remove the field from doc

`POST` student/\_update/<doc_id>

```json
{
    "script": {
        "source": "ctx._source.remove('qualifications')"
    }
}
```

#### Replace the document with new fields

`PUT` student/\_doc/<doc_id>

```json
{
    "name": "Mohd Ubaid Khan",
    "designation": "Software Developer",
    "qualification": "BCA",
    "age": 23
}
```
