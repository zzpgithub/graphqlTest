# graphqlTest
1. Query
```
{
  allLinks {
    url
    description
  }
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
查询一个link:
```
{
  allLinks {
    url
    description
  }
  link(id: 0){
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
      }
    ],
    "link": {
      "url": "http://howtographql.com",
      "description": "Your favorite GraphQL page"
    }
  }
}
```
2. Mutation
```
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
```
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
