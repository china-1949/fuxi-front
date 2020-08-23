<template>
  <!-- 自定义的组件 -->
  <div id="button-counter">
      <span>name</span>
      <!-- 预先留出的插槽，提供位置 -->
      <slot></slot>
      <!-- v-on监听 -->
      <button @click="count++">--{{propName}}点击了我{{count}}次 </button>
        <button @click="addcount">--{{propName}}点击了我{{count1}}次 </button>

  </div>
</template>

<script>

export default {
  name: 'button-counter',
  props:['propName'],  //传入参数 来自App.vue里面的data属性
  data () {
    return {
      count:0,
      count1:0

    }
  },
  methods:{// 方法
    addcount(){
      this.count1= this.count1+1;
  },
},
}
</script>

<style lang="scss">

</style>
