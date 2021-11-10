<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="number" v-model="state.num1"><span>+</span>
    <input type="number" v-model="state.num2"><span>=</span>
    <span>{{state.result}}</span>
    <button @click="clickData">子传父</button>
  </div>
</template>

<script>
// import { ref } from 'vue'
import { reactive,computed,onMounted,onRenderTracked,onRenderTriggered,onUpdated } from 'vue'
export default {
  props: {
    msg: {
      type: String,
      required: true
    }
  },
  beforeCreate(){
    console.log('beforeCreate');
  },
  created(){
    console.log('created');
  },
  mounted(){
    console.log('mounted');
  },
  // setup (props) {
  //   console.log(props) // { user: '' }
  //   const num1 = ref(0)
  //   const num2 = ref(0)
  //   const result = ref(0)
  //   function add(){
  //     result.value=num1.value+num2.value
  //   }
  //   return {
  //     num1,num2,result,add
  //   } // 这里返回的任何内容都可以用于组件的其余部分
  // }
  setup(props, {emit}){
    console.log(props,'props');
    const state = reactive({
      num1:0,
      num2:0,
      result:computed(()=>state.num2+state.num1)
    })
    onMounted(() => {
      console.log('Component is mounted!')
    })
    onRenderTracked((e) => {
      console.log('Component is onRenderTracked!',e)
    })
    onRenderTriggered((e) => {
      console.log('Component is onRenderTriggered!',e)
    })
    onUpdated(() => {
      console.log('Component is onUpdated!')
    })
    // function add() {
    //   state.result = state.num1+state.num2
    // }
    function clickData(){
      console.log('clickData');
      emit('msg',state.result)
    }
    return {
      state,
      clickData
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
