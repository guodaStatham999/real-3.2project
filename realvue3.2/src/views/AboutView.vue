<template>
  <div class="about">
    <h1>This is an new generatation</h1>
    my name is {{info.name}}<br>
    my age is {{info.age}}
  </div>
  <button @click="toChi('AboutViewChi')">to router child</button>
  <AboutChild v-model:key1="key1"  v-model:value2="value2" :list='list' @add='addList' ></AboutChild>
  <router-view></router-view>
</template>


<script lang="ts" setup>
import { reactive, ref,computed,watch } from 'vue';
import { Options, Vue } from 'vue-class-component';
import { useRouter  } from 'vue-router';
import AboutChild from '../components/AboutComponentChild'

let router = useRouter()
let info = reactive({
  name:'tkf',
  age:18
})
let time = ref(10)
setTimeout(()=>{
  time.value = 999
},1000)
watch(time,(newVal,oldVal)=>{
  // console.log(newVal,'newVal',oldVal,'oldVal');
  
})
setTimeout(()=>{
  info.name = '你好,vue3.2'
},1000)
watch(()=>info.name,(newVal,oldVal)=>{
  // console.log('newVal',newVal,'oldVal',oldVal);
})
let notChangeCompute = ref(0)
let finalCount = computed(()=>notChangeCompute.value + 1)
// console.log(notChangeCompute);
// console.log(finalCount);
function toChi(params:string) {
  router.push({
    name:params
  })
}

// 页面v-model
    const key1 = ref("1111")
    const value2 = ref("2222")
// 列表逻辑
let list = ref([
  {
    name:'tkf1',
    age:222
  },
  {
    name:'tkf2',
    age:222
  },
  ])
  function addList(val){
    console.log(val);
    list.value.push({
      name:val,
      age:val
    })
    
  }

</script>