# graphqlTest
文档： https://www.howtographql.com/graphql-java/0-introduction/

核心概念： https://segmentfault.com/a/1190000014131950
##1. Query（查询）
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
##2. Mutation(更改)
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
##3. Connectors
###3.1 mongoDB
 + 学习连接 http://www.runoob.com/mongodb/mongodb-create-collection.html
 + 安装https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/
 + terminal中启动mongoDB \
   ```-> mongod``` 
 + 再新终端中，连接mongoDB
   ```
   -> mongo
   MongoDB shell version v4.0.3
   connecting to: mongodb://127.0.0.1:27017
   Implicit session: session { "id" : UUID("c9c3517b-4ac6-4788-a61a-e9fe1ddb9e55") }
   MongoDB server version: 4.0.3
   ```
 + 运行工程： ```mvn jetty:run```, 在GraphiQL ```http://localhost:8080/```中输入：
   ```
   mutation createLink {
     createLink(url: "http://www.graph.cool", description: "Serverless GraphQL Backend"){
     	url
     	description
     }
   }
   ```
   从而将数据保存至mongoDB中.
 + 查看所有数据库：
   ```
   > show dbs
   admin       0.000GB
   config      0.000GB
   hackernews  0.000GB #创建的数据库
   local       0.000GB
   ```
 + 如果要查看已有集合，可以使用 show collections 命令：
    ```
    > use hackernews
    switched to db hackernews
    > show collections
    links
    > db.links.find().pretty() #查看集合中的数据
    {
    	"_id" : ObjectId("5bdbc255b4ea083d1325e013"),
    	"url" : "http://www.graph.cool",
    	"description" : "Serverless GraphQL Backend"
    }
    ```
 ##Authentication
 
 ###create users
 ```
 mutation createUser {
   createUser(
     name: "Bojack Horseman"
     authProvider: {
       email: "bojack@example.com"
       password: "secret"
     }
   )
   {
     id
     name
   }
 }
 ```
 结果：
 ```
 {
   "data": {
     "createUser": {
       "id": "5bdc04cfc6e3e33fa0205165",
       "name": "Bojack Horseman"
     }
   }
 }
 ```
 