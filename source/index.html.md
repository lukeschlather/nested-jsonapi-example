## <a name="resource-person">Person</a>

Stability: `prototype`

A person (living, breathing human being).


### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **data:attributes:email** | *email* | email address | `"username@example.com"` |
| **data:attributes:first-name** | *string* | first name | `"Sigurd"` |
| **data:attributes:last-name** | *string* | last name | `"Kuhn"` |
| **data:attributes:middle-name** | *string* | middle name | `"Graham"` |
| **data:attributes:phone-numbers/label** | *string* | phone number label | `"home"` |
| **data:attributes:phone-numbers/number** | *string* | fully qualified phone number | `"+12065558971x12100"` |
| **data:id** | *uuid* | unique identifier of a person | `"01234567-89ab-cdef-0123-456789abcdef"` |
| **[data:relationships:revision:data:id](#resource-revision)** | *uuid* | unique identifier of a revision | `"01234567-89ab-cdef-0123-456789abcdef"` |
| **[data:relationships:revision:data:type](#resource-revision)** | *string* | the revision type<br/> **one of:**`"revisions"` | `"revisions"` |
| **data:type** | *string* | the people type<br/> **one of:**`"people"` | `"people"` |

### Person Create

Create a new person.


```
POST /people
```

#### Optional Parameters

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **data:attributes:email** | *email* | email address | `"username@example.com"` |
| **data:attributes:first-name** | *string* | first name | `"Sigurd"` |
| **data:attributes:last-name** | *string* | last name | `"Kuhn"` |
| **data:attributes:middle-name** | *string* | middle name | `"Graham"` |
| **data:attributes:phone-numbers/label** | *string* | phone number label | `"home"` |
| **data:attributes:phone-numbers/number** | *string* | fully qualified phone number | `"+12065558971x12100"` |
| **data:id** | *uuid* | unique identifier of a person | `"01234567-89ab-cdef-0123-456789abcdef"` |
| **data:type** | *string* | the people type<br/> **one of:**`"people"` | `"people"` |


#### Curl Example

```bash
$ curl -n -X POST https://api.example.com/accounts/people \
  -d '{
  "data": {
    "type": "people",
    "id": "01234567-89ab-cdef-0123-456789abcdef",
    "attributes": {
      "first-name": "Sigurd",
      "middle-name": "Graham",
      "last-name": "Kuhn",
      "email": "username@example.com",
      "phone-numbers": [
        {
          "label": "home",
          "number": "+12065558971x12100"
        }
      ]
    }
  }
}' \
  -H "Content-Type: application/vnd.api+json"
```


#### Response Example

```
HTTP/1.1 201 Created
```

```json
{
  "data": {
    "type": "people",
    "id": "01234567-89ab-cdef-0123-456789abcdef",
    "attributes": {
      "first-name": "Sigurd",
      "middle-name": "Graham",
      "last-name": "Kuhn",
      "email": "username@example.com",
      "phone-numbers": [
        {
          "label": "home",
          "number": "+12065558971x12100"
        }
      ]
    },
    "relationships": {
      "revision": {
        "data": {
          "type": "revisions",
          "id": "01234567-89ab-cdef-0123-456789abcdef"
        }
      }
    }
  }
}
```

### Person Info

Info for an existing person.


```
GET /people/{person_id}
```


#### Curl Example

```bash
$ curl -n https://api.example.com/accounts/people/$PERSON_ID \
 -G \
  -d  \
  -H "Content-Type: application/vnd.api+json"
```


#### Response Example

```
HTTP/1.1 200 OK
```

```json
{
  "data": {
    "type": "people",
    "id": "01234567-89ab-cdef-0123-456789abcdef",
    "attributes": {
      "first-name": "Sigurd",
      "middle-name": "Graham",
      "last-name": "Kuhn",
      "email": "username@example.com",
      "phone-numbers": [
        {
          "label": "home",
          "number": "+12065558971x12100"
        }
      ]
    },
    "relationships": {
      "revision": {
        "data": {
          "type": "revisions",
          "id": "01234567-89ab-cdef-0123-456789abcdef"
        }
      }
    }
  }
}
```

### Person List

List existing people.


```
GET /people
```

#### Optional Parameters

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **filter[changed-since]** | *date-time* |  | `"2015-01-01T12:00:00Z"` |


#### Curl Example

```bash
$ curl -n https://api.example.com/accounts/people \
 -G \
  -d filter[changed-since]=2015-01-01T12%3A00%3A00Z \
  -H "Content-Type: application/vnd.api+json"
```


#### Response Example

```
HTTP/1.1 200 OK
```

```json
{
  "data": [
    {
      "type": "people",
      "id": "01234567-89ab-cdef-0123-456789abcdef",
      "attributes": {
        "first-name": "Sigurd",
        "middle-name": "Graham",
        "last-name": "Kuhn",
        "email": "username@example.com",
        "phone-numbers": [
          {
            "label": "home",
            "number": "+12065558971x12100"
          }
        ]
      },
      "relationships": {
        "revision": {
          "data": {
            "type": "revisions",
            "id": "01234567-89ab-cdef-0123-456789abcdef"
          }
        }
      }
    }
  ]
}
```

### Person Batch Create

Create a group of people together with an import tag.
Warning! This is not currently JSON API compliant until a bulk extension is
standardized.


```
POST /people/batches/{revision_import-tag}
```

#### Optional Parameters

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **data** | *array* |  | `[{"type":"people","id":"01234567-89ab-cdef-0123-456789abcdef","attributes":{"first-name":"Sigurd","middle-name":"Graham","last-name":"Kuhn","email":"username@example.com","phone-numbers":[{"label":"home","number":"+12065558971x12100"}]}}]` |


#### Curl Example

```bash
$ curl -n -X POST https://api.example.com/accounts/people/batches/$REVISION_IMPORT-TAG \
  -d '{
  "data": [
    {
      "type": "people",
      "id": "01234567-89ab-cdef-0123-456789abcdef",
      "attributes": {
        "first-name": "Sigurd",
        "middle-name": "Graham",
        "last-name": "Kuhn",
        "email": "username@example.com",
        "phone-numbers": [
          {
            "label": "home",
            "number": "+12065558971x12100"
          }
        ]
      }
    }
  ]
}' \
  -H "Content-Type: application/vnd.api+json"
```


#### Response Example

```
HTTP/1.1 202 Accepted
```



## <a name="resource-revision">Revision</a>

Stability: `prototype`

Revisions are linked from all other objects to be able to reference when a
particular resource was made along with any possible metadata.


### Attributes

| Name | Type | Description | Example |
| ------- | ------- | ------- | ------- |
| **data:attributes:created-at** | *date-time* | when this import tag was created | `"2015-01-01T12:00:00Z"` |
| **data:attributes:import-tag** | *string* | a tag to represent an import operation | `"example"` |
| **data:id** | *uuid* | unique identifier of a revision | `"01234567-89ab-cdef-0123-456789abcdef"` |
| **data:type** | *string* | the revision type<br/> **one of:**`"revisions"` | `"revisions"` |


