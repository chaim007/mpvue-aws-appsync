
# 安装依赖
$ npm install
# 运行
$ npm run dev

 DONE  Compiled successfully in 6752ms                                  13:04:16
 
 打开微信开发客户端，新建项目---> 打开dist目录！

# 后台准备
开通和使用亚马逊的appsync服务，具体开通方法可以自行谷歌下哈。

# shema文件
下面是schema文件内容，贴到appsync控制台即可。

# 修改appSync.js文件为你自己的配置

export default {
  graphqlEndpoint: 'https://uezbpno7qngrbdtxzfuuuelfvu.appsync-api.us-east-2.amazonaws.com/graphql',
  region: 'us-east-2',
  authenticationType: 'API_KEY',
  apiKey: 'da2-e7nqmnzl6ffqxhf32tav5crhz4',
};
