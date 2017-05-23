# 写一个简单的页面


* **1.** 用WebStorm ,Atom 或者其他编辑工具打开种子工程

* **2.** 新建component文件编写组件和样式

```
<template>
  <div class="workflow-list">
    <a class="workflow-list-item">
      <div class="workflow-list-logo">
        <img :src="icon"/>
      </div>
      <div class="workflow-list-header">{{title}}</div>
      <div class="workflow-list-content">
        <div class="row no-padding">
          <div class="col col-90 no-padding">
            <div class="row no-padding">
              <div class="col col-33 no-padding color-type">{{type}}</div>
              <div class="col col-67 no-padding color-content">{{typeValue}}</div>
            </div>
            <div class="row no-padding">
              <div class="col col-33 no-padding color-type">{{node}}</div>
              <div class="col col-67 no-padding color-content">{{nodeValue}}</div>
            </div>
            <div class="row no-padding">
              <div class="col col-33 no-padding color-type">{{submit}}</div>
              <div class="col col-67 no-padding color-content">{{submitPerson}}</div>
            </div>
            <div class="row no-padding" v-if="showExtraFlag">
              <div class="col col-33 no-padding color-type">{{key1}}</div>
              <div class="col col-67 no-padding color-content">{{value1}}</div>
            </div>
            <div class="row no-padding" v-if="showExtraFlag">
              <div class="col col-33 no-padding color-type">{{key2}}</div>
              <div class="col col-67 no-padding color-content">{{value2}}</div>
            </div>
            <div class="row no-padding" v-if="showExtraFlag">
              <div class="col col-33 no-padding color-type">{{key3}}</div>
              <div class="col col-67 no-padding color-content">{{value3}}</div>
            </div>
          </div>
          <div class="col col-10 no-padding col-center workflow-list-select">
            <img src="../assets/images/select.png"/>
          </div>
        </div>
      </div>
    </a>
  </div>
</template>
<style lang="scss">
  .workflow-list {
    position: relative;
    background: white;
    margin-top: 10px;
    margin-left: 18px;
    margin-right: 5px;
    border-bottom-right-radius: 25px;
    box-shadow: 0px 0px 4px #D2D2D2;

    .workflow-list-item {
      display: block;
      &.activated {
        background: #f8f8f8;
      }
    }

    &.item {
      overflow: visible;
    }
    .item-content {
      overflow: visible;
      border-bottom-right-radius: 25px;
      padding: 0px;
      border: none;
    }

    .item-options .button {
      border-bottom-right-radius: 25px;
    }

    .color-title {
      color: #1F8CEB;
    }
    .color-type {
      font-weight: bold;
      font-size: 14px;
      color: #4A4A4A;
    }
    .color-content {
      font-size: 14px;
      color: #4A4A4A;
      overflow: hidden;
      white-space: nowrap;
      white-space: pre-wrap;
    }

    .no-padding {
      padding: 0;
      margin: 0;
    }

    .workflow-list-logo {
      height: 50px;
      width: 50px;
      border-radius: 25px;
      padding: 4px;
      background: white;
      position: absolute;
      top: -5px;
      left: -12px;
      img {
        height: 42px;
        width: 42px;
        border-radius: 21px;
      }
    }

    .workflow-list-header {
      margin-left: 55px;
      height: 40px;
      line-height: 40px;
      border-bottom: 2px dotted #D2D2D2;
      color: #1F8CEB;
    }
    .workflow-list-content {
      padding: 12px;
      .workflow-list-select {
        img {
          float: right;
          width: 28px;
          height: 28px;
        }
      }
    }
  }
</style>
<script>
  export default{
    props: {
      showExtraFlag: {
        type: Boolean,
        default: false
      },
      icon: {type: String,default: require('../assets/images/add.png')},
      title: {type: String,default: ''},
      type: {type: String,default: ''},
      typeValue: {type: String,default: ''},
      node: {type: String,default: ''},
      nodeValue: {type: String,default: ''},
      submit: {type: String,default: ''},
      submitPerson: {type: String,default: ''},
      key1: {type: String,default: ''},
      value1: {type: String,default: ''},
      key2: {type: String,default: ''},
      value2: {type: String,default: ''},
      key3: {type: String,default: ''},
      value3: {type: String,default: ''}
    },
    methods: {
    }
  }
</script>
```

* **3.** 配置路由，随便配置任易路由，在mounted()方法里面可以编写程序逻辑

```
import Main from './views/main';

或者

const Main = resolve =>{
 require.ensure(['./views/main'], () => {
 resolve(require('./views/main'));
 });
 };
```

* **4.** 在主界面使用组件并完成第一个Demo,此时已经可以运行Demo。

```
<template>
  <div class="main-home">
    <base-loading v-if="isLoadingData"></base-loading>
    <div v-if="!isLoadingData">
      <workflow-list v-for='item in workflowList'
                     :title='item.title'
                     :icon='item.icon'
                     :type='item.type'
                     :type-value='item.typeValue'
                     :node='item.node'
                     :nodeValue='item.nodeValue'
                     :submit='item.submit'
                     :submiPperson='item.submitPerson'
                     :showExtraFlag="showExtraFlag">
      </workflow-list>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import {Tab, TabItem, Sticky, Divider, XButton, Swiper, SwiperItem} from 'vux'
  import WorkflowList from '../components/workflow-list.vue';
  import baseLoading from '../components/base-loading.vue';

  export default {
    components: {
      Tab,
      TabItem,
      Sticky,
      Divider,
      XButton,
      Swiper,
      SwiperItem,
      WorkflowList,
      baseLoading
    },
    data () {
      return {
        isLoadingData: true,
        showExtraFlag: false,
        workflowList: []
      }
    },
    methods: {
    },
    mounted(){
    }
  }
</script>
```