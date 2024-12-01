# Analysis

-   Analysis refers to the process of converting text into
    terms that can be efficiently stored and searched

-   Elasticsearch uses a powerful text analysis engine to
    break down textual data into individual tokens or
    terms, which are then used to build an inverted index
    for fast and accurate full-text search.

### Analysis steps

**Character Filters:** Character filters are used to process the
input text before tokenization. They can
perform tasks like removing HTML tags,
replacing specific characters,etc.

**Tokenization:** Standard Tokenizer (splits the text into words based on whitespace and punctuation).

**Token Filtering:** Lowercase Token Filter (converts all tokens to lowercase).

`POST` analyze

```json
{
    "text": "Hello,How are you ? What's up ? This is so high-end",
    "analyzer": "standard"
}
```

#### Breakdown of standard analyzer into char_filter, tokenizer and filter

`POST` analyze

```json
{
    "text": "Hello,How are you ? What's up ? This ts so high-end",
    "char_filter": {},
    "tokenizer": "standard",
    "filter": ["lowercase", " stop"]
}
```

# Inverted index

-   An inverted index is a fundamental data structure used to
    efficiently store and retrieve information from a large collection of
    documents. It is the backbone of Elasticsearch's powerful and fast
    full-text search capabilities.

-   The inverted index is designed to solve the
    problem of quickly finding all documents
    that contain a specific term or word in a
    vast collection of documents.

-   Instead of scanning through each
    document one by one, which can be time-
    consuming for large datasets, the inverted
    index allows Elasticsearch to perform
    searches much more efficiently.

-   For each token, the inverted index maintains a
    list of document IDs where the token appears.
    It creates a mapping between each token and
    the corresponding documents that contain
    that token.

-   Maps terms to the documents they appear in. It is widely used in
    modern search engines like Elasticsearch for efficient full-text
    search and retrieval.

#### Example

Document 1: "The quick brown fox"  
Document 2: "Jumped over the lazy dog"  
Document 3: "The fox and the dog"

| Token  | Document Id |
| ------ | ----------- |
| and    | 3           |
| brown  | 1           |
| dog    | 2, 3        |
| fox    | 1, 3        |
| jumped | 2           |
| lazy   | 2           |
| over   | 2           |
| quick  | 1           |
| the    | 1, 3        |

-   Now, when you search for a term like "fox,"
    Elasticsearch can quickly look up the term in
    the inverted index and retrieve the document
    IDs [1 3], which correspond to the documents
    containing the term "fox."

-   Bv leveraging the inverted index, Elasticsearch
    dramatically reduces the time and resources required
    to perform complex searches over large sets of
    documents, making it a powerful tool for building
    search applications and systems.
