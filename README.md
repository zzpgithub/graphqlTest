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

2. Mutation
```json
mutation createLink {
  createLink(url: "http://www.graph.cool", description: "Serverless GraphQL Backend"){
  	url
  	description
  }
}
```
执行结果：
```json
{
     "data": {
       "createLink": {
         "url": "http://www.graph.cool",
         "description": "Serverless GraphQL Backend"
       }
     }
   }
```

再查询：
```json
{
  allLinks {
    url
    description
  }
}
```
查询结果：
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
      },
      {
        "url": "http://www.graph.cool",
        "description": "Serverless GraphQL Backend"
      }
    ]
  }
}
```