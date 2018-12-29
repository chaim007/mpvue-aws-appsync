
# 安装依赖
$ npm install
# 运行
$ npm run dev

 DONE  Compiled successfully in 6752ms                                  13:04:16
 
 打开微信开发客户端，新建项目---> 打开dist目录！

# 后台准备
开通和使用亚马逊的appsync服务，具体开通方法可以自行谷歌下哈。

# shema文件，并创建dataSource
下面是schema文件内容，贴到appsync控制台即可。

    input CreateTaskInput {
      id: ID!
      name: String!
      completed: Boolean!
    }

    input DeleteTaskInput {
      id: ID!
    }

    type Mutation {
      createTask(input: CreateTaskInput!): Task
      updateTask(input: UpdateTaskInput!): Task
      deleteTask(input: DeleteTaskInput!): Task
    }

    type Query {
      do(id: ID!): Task
      getTask(id: ID!): Task
      listTasks(first: Int, after: String): TaskConnection
    }

    type Subscription {
      onCreateTask(id: ID, name: String, completed: Boolean): Task
        @aws_subscribe(mutations: ["createTask"])
      onUpdateTask(id: ID, name: String, completed: Boolean): Task
        @aws_subscribe(mutations: ["updateTask"])
      onDeleteTask(id: ID, name: String, completed: Boolean): Task
        @aws_subscribe(mutations: ["deleteTask"])
    }

    type Task {
      id: ID!
      name: String!
      completed: Boolean!
    }

    type TaskConnection {
      items: [Task]
      nextToken: String
    }

    input UpdateTaskInput {
      id: ID!
      name: String
      completed: Boolean
    }


# 修改appSync.js文件为你自己的配置

    export default {
      graphqlEndpoint: 'https://uezbpno7ccccZ*****.amazonaws.com/graphql',
      region: 'us-east-2',
      authenticationType: 'API_KEY',
      apiKey: 'da2-%%%%%%********',
    };
