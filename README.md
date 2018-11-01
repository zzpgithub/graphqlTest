# graphqlTest
1. Query
```java
schema {
    query: Query
    mutation: Mutation
}
```
result:
```json
{
  "data": {
    "allLinks": [
      {
        "url": "http://howtographql.com",
        "description": "Your favorite GraphQL page"
      },
      {
        "url": "http://graphql.org/learn/",
        "description": "The official docks"
      }
    ]
  }
}
```