<template>
  <div class="about">
    <div id="container"></div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import AMapLoader from '@amap/amap-jsapi-loader';
import { shallowRef } from '@vue/reactivity'
export default defineComponent({
  setup() {
    console.log('setup')
    const map = shallowRef(null);
    
    return {
      map,
    }
  },
  created(){
    console.log('created')
  },
  mounted() {
    console.log('mounted')
    //DOM初始化完成进行地图初始化
    this.initMap();
  },
  methods: {
    initMap() {
      AMapLoader.load({
        key: "b394514f637c7102805858e4bae01c79",             // 申请好的Web端开发者Key，首次调用 load 时必填
        version: "2.0",      // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
        plugins: [''],       // 需要使用的的插件列表，如比例尺'AMap.Scale'等
      }).then((AMap) => {
        this.map = new AMap.Map("container", {  //设置地图容器id
          viewMode: "3D",    //是否为3D地图模式
          zoom: 5,           //初始化地图级别
          center: [105.602725, 37.076636], //初始化地图中心点位置
        });
      }).catch(e => {
        console.log(e);
      })
    },
  },
})
</script>

<style>
@media (min-width: 1024px) {
  .about {
    /* min-height: 100vh; */
    display: flex;
    align-items: center;
  }

  #container {
    padding: 0px;
    margin: 0px;
    width: 100%;
    height: 800px ;
  }
}
</style>
