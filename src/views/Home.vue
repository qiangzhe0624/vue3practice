<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" @msg="getMsg"/>
  </div>
  强者
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src

@Options({
  components: {
    HelloWorld,
  },
  setup(){
    console.log('homesetup');
    
  },
  methods:{
    getMsg(result:number){
      console.log(result,'result');
      
    }
  }
})
export default class Home extends Vue {}
</script>
