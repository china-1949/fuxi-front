<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <h1>{{ msg1 }}</h1>
    <!-- 单项绑定  type指定绑定input的类型 text和button-->
    <input v-bind:type="type" v-bind:value="msg" />
    <!--缩写：  -->
      <input :type="type" :value="msg" />
      <!--双向绑定 data里面的值也会跟着变化 会显指定也会变化-->
      <input v-model="msg1" />

      <!--监听 简写v-on：就是@-->
      <button @click="changeMsg">click me</button>

      firstname:<input v-model="firstname" />
      lastname:<input v-model="lastname" />
      fulname:{{firstname}}&nbsp; {{lastname}}<br/>
      fulname:methods:{{getFullname()}}<br/>   <!--双大括号可以调用方法-->
      fulname:computed:{{fullname}}<br/>
      fulname:watch:{{fullnameWatch}}<br/>

      <!-- 条件 加显示判断-->
        <h1 v-if="flag">{{ msg }}</h1>

        <h1 v-if="flag1>1">11111111</h1>
        <h1 v-else-if="flag1==1">111111sssss11</h1>
        <h1 v-else>7777</h1>

        <!-- v-show控制显示问题 和上面的v-if的boolean类型一致的  v-show在F12审查还存在<h1 style="display: none;">this is vue.js App</h1>-->
            <h1 v-show="flag">{{ msg }}</h1>

            <!-- 数据的遍历 -->
            <h1 v-for="item in list">{{item}}</h1>
            <!-- 使用：key绑定可以提高遍历效率 -->
            <h1 v-for="(item,index) in list" :key="index">{{item}} --  {{index}} </h1>
            <br/>
            <!-- 练习 -->
            <input v-model="name" /><button @click="addUser">添加</button></br>
            <ol>
              <li v-for="(item,index) in userList" :key="index">
                  <span v-if="index % 3 == 0" class="red">{{item}}</span>
                  <span v-else-if="index % 3 == 1" class="green">{{item}}</span>
                  <span v-else  class="blue">{{item}}</span>

              </li>
            </ol>
            <!-- 组件相互独立的互不干扰 -->
            <button-counter :prop-name='a'>
              <span>A</span>
              <span>dsfsdfs</span>
              <span>dsfsdfs</span>
              <span>dsfsdfs</span>
            </button-counter>

            <button-counter :prop-name='b'>
                <span>B</span>
            </button-counter>

            <button-counter :prop-name='c'></button-counter>
            <button-counter :prop-name='d'></button-counter>

            <!-- 引入button-counter  id为 button-counter 相互独立的不影响  -->
            <!-- 在 ButtonCounter预留了插槽，这个插槽我们在app.vue中可以添加自己的一些东西-->
          <!--  prop-name="a" 传递参数  还需要v-bind绑定data中的值-->
          <!-- 发现参数的大小写是存在差异的 -->
             <button-counter prop-name="a">
                <span>dsfsdfs</span>
                <span>dsfsdfs</span>
                <span>dsfsdfs</span>

            </button-counter>
            <button-counter prop-name="b"></button-counter>
            <button-counter prop-name="c"></button-counter>
            <button-counter prop-name="d"></button-counter>



  </div>
</template>

<script>
// button-counter引入
import ButtonCounter from './components/ButtonCounter'
export default {
  name: 'app',
  // 暴露components下的ButtonCounter
  components:{
    ButtonCounter
  },
  data () {
    return {
      msg: 'this is vue.js App',
      msg1: 'this is vue.js App1111111',
       type:"button",
    //  type:"text",
      firstname:'Andy',
      lastname:'Zheng',
      fullnameWatch:'Andy Zheng',
      flag:false,
      flag1:-343,
      list:[111,222,333],
      name:'',
      userList: [],
      a:'A',
      b:'B',
      c:'C',
      d:'D'

    }
  },
  methods:{// 方法
    addUser(){
    //  debugger
      this.userList.push(this.name)
      this.name='';
    },
    changeMsg(){
    //  alert('msg');
    this.msg = 'andy';
  },
  getFullname(){
    return this.firstname + ' ' + this.lastname;
  }
},
computed:{ //计数结果在缓存里面，效率高
    fullname: function(){
      return this.firstname + ' ' + this.lastname;
    }

    // fullname(){
    //   return this.firstname + ' ' + this.lastname;
    // }
},
// 一般监听输入，变化改变data值，指定回显也会变化
watch:{
  firstname(val){
    console.log(val);
    return this.fullnameWatch = val+' '+this.lastname;
  },
  lastname(val){
    console.log(val);
      return this.fullnameWatch = this.firstname+' '+val;
  }
}
}
</script>

<style lang="scss">
  .red{
    background-color: #ff0000;
  }
  .green{
    background-color: #00ff00;
  }
  .blue{
    background-color: #0000ff;
  }
</style>
