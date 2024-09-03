# survey-plat(问卷调研系统)

#### 介绍

一款功能强大的调研问卷系统；有多种题型可供选择，拖动即可生成，支持在线预览，报表查询等。支持题目之间相互跳转和显示。社区版已上线🎉🎉🎉，部分功能正在更新中。。。敬请期待！！！

[功能更新日志](./UPDATE.md)

[官网：http://120.27.230.112:8200/ ](http://120.27.230.112:8200 "去体验")(账号密码：admin/123456)

注：测试账号可供任何人使用，请大家操作时应遵守相关法律法规，如产生违法违规行为作者不承担相关法律责任。

[在线体验：http://120.27.230.112:8200/surveyFront/?surveyCode=66cc1df675b18761c2e580e8#/](http://120.27.230.112:8200/surveyFront/?surveyCode=66cc1df675b18761c2e580e8#/ "在线体验")

需要您的 star ⭐️⭐️⭐️ 支持鼓励 🙏🙏🙏， **右上角点 Star 加 QQ 群(463834000) 获取详细信息** 。

QQ群：463834000

支持独立部署，微前端集成，数据对接，sass服务。如需商业支持请加QQ：1256598178。

如有问题可提Issues。

本项目可使用微前端集成答题端，方便更加灵活的适应各种场景，操作步骤请按以下方式实现（下面以vue方式集成为例。注：微应用不受前端框架影响，均可集成。）：

> npm i qiankun -D

```
// microAction.js

import { initGlobalState } from 'qiankun';

const initialState = {};
const actions = initGlobalState(initialState);

export default actions;

```

```
// demo.vue

<template>
  <div>
    <div id="survey_demo" />
    <el-button @click="submit">提交</el-button>
  </div>
</template>

<script>
import { loadMicroApp } from 'qiankun';
import MicroAction from './microAction.js'
export default {
  data() {
    return {
      microApp: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.microApp = loadMicroApp({
        name: 'survey_front_app_enter',
        entry: `http://120.27.230.112:8081/surveyFrontMicro/`,
        container: '#survey_demo',
        props: {
          surveyCode: '66cc1df675b18761c2e580e8', // 对应生成平台的surveyCode
        }
      })

      MicroAction.onGlobalStateChange((state, prev) => {
        if (state.sendBody !== 'microApp') return
        console.log('主应用', state);
      });
      MicroAction.setGlobalState({
        sendBody: 'parentApp', // 发消息的是哪个应用 parentApp是父应用、microApp是微应用（详细信息可加群咨询）
        eventType: 'lifeCycle', // 生命周期类型（详细信息可加群咨询）
        eventName: 'onInit', // 初始化完成（详细信息可加群咨询）
      })
    })
  },
  beforeDestroy() {
    this.microApp?.unmount?.()
  },
  methods: {
    submit() {
      MicroAction.setGlobalState({
        sendBody: 'parentApp',
        eventType: 'click',
        eventName: 'questionSave',
      })
    }
  },
}
</script>

```

### 管理端

![管理端](https://huimei-edc.oss-cn-shanghai.aliyuncs.com/edc/data/image/upload_to_oss_component/survey/home.png)

### 生成平台

![1724921417755](https://huimei-edc.oss-cn-shanghai.aliyuncs.com/edc/data/image/upload_to_oss_component/survey/desk20240829163744.png)

### 预览

![1724921417755](https://huimei-edc.oss-cn-shanghai.aliyuncs.com/edc/data/image/upload_to_oss_component/survey/proview_20240829163824.png)

### 答题端

![1724921417755](https://huimei-edc.oss-cn-shanghai.aliyuncs.com/edc/data/image/upload_to_oss_component/survey/answer_20240829164836.png)

### 报表功能

![1724921417755](https://huimei-edc.oss-cn-shanghai.aliyuncs.com/edc/data/image/upload_to_oss_component/survey/data_20240829164353.png)
![1724921417755](https://huimei-edc.oss-cn-shanghai.aliyuncs.com/edc/data/image/upload_to_oss_component/survey/data_20240829164407.png)
