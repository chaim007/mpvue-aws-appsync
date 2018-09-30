<template>
<div>  
  <task> </task>
</div>

</template>

<script>
import task from '@/components/tasks';
import Vue from 'vue';
import { AWSAppSyncClient, createAppSyncLink } from 'aws-appsync';
import VueApollo from 'vue-apollo';
import wxFetch from 'wxapp-fetch';
import { HttpLink } from 'apollo-link-http';
import appSyncConfig from '../../AppSync';

const config = {
  disableOffline: true,
};

const uri = appSyncConfig.graphqlEndpoint;
const resultsFetcherLink = new HttpLink({ uri, fetch: wxFetch });
const link = createAppSyncLink({
  url: uri,
  region: appSyncConfig.region,
  auth: {
    type: appSyncConfig.authenticationType,
    apiKey: appSyncConfig.apiKey,
  },
  resultsFetcherLink,
});

const options = {
  link,
  defaultOptions: {
    watchQuery: {
      fetchPolicy: 'cache-and-network',
    },
  },
};

const client = new AWSAppSyncClient(config, options);
const appsyncProvider = new VueApollo({
  defaultClient: client,
}).provide();

Vue.config.productionTip = false;
Vue.use(VueApollo);

export default {
  components: {
    task,
  },
  provide: appsyncProvider,
};
</script>

<style scoped>
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 150px;
}

.form-control {
  display: block;
  padding: 0 12px;
  margin-bottom: 5px;
  border: 1px solid #ccc;
}

.counter {
  display: inline-block;
  margin: 10px auto;
  padding: 5px 10px;
  color: blue;
  border: 1px solid blue;
}
</style>
