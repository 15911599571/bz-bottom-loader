<template>
  <doc name="bz-bottom-loader"
    desc="拉到底部加载"
    parm_desc="滚动到底部以后，加载更多内容(dom没有屏幕长，是无法触发的，以后修正)"
    :parms="parms"
    :code="code"
    >
    <div class="ui grid">
      <div  v-for="data in datas" class="sixteen wide column">
        <div class="ui card">
          <div class="content">
            <a class="description">{{data}}</a>
          </div>
        </div>
      </div>
    </div>
    <bottom-loader element_class=".ui.card" v-on:bottom="call_back"></bottom-loader>
  </doc>
</template>

<script>
  import BottomLoader from './Bz'
  import Doc from 'bz-doc'
  export default {
    components: {
      BottomLoader,
      Doc
    },
    data: function () {
      return {
        datas: [1],
        parms: [
          {parm: 'element_class', desc: '用于定位last的class .hah.jj 的格式'},
          {parm: 'v-on:bottom', desc: '事件触发, 滚到底部的回调函数'}
        ],
        parm_desc: `注意，如果使用的组件有路由，那么最好在切换路由的时候发送消息，解除绑定(参看本例子) <code>this.$broadcast('unbind-scroll')</code>`,
        code: `<bottom-loader element_class=".ui.card" v-on:bottom="call_back"></bottom-loader>`
      }
    },
    methods: {
      call_back: function () {
        this.datas.push(this.datas.length + 1)
      }
    }
  }
</script>
