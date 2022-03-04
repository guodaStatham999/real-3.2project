<template>
  <div class="about">
    <h1>This is an new generatation</h1>
    <button @click="toggleTabl">切换为表格</button>

  </div>

  <aboutChildTable v-if='isShowTable' ></aboutChildTable>
  <AboutChild v-else ref='childRef' v-model:key1="key1"  v-model:value2="value2" :list='list' @add='addList' ></AboutChild>
  <div v-if='!isShowTable'>
          my name is {{info.name}}<br>
    my age is {{info.age}}
  <button @click="toChi('AboutViewChi')">to router child</button>
  </div>
  <router-view></router-view>
</template>


<script lang="ts" setup>
import { reactive, ref,computed,watch,provide, shallowRef } from 'vue';
import { Options, Vue } from 'vue-class-component';
import { useRouter  } from 'vue-router';
import AboutChild from '../components/AboutComponentChild'
import aboutChildTable from '../components/aboutChildTable'
let isShowTable = ref(false)
let toggleTabl = ()=>{
  isShowTable.value = !isShowTable.value
}

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

// 获取元素
let childRef = ref(null)
// setTimeout(()=>{
//   console.log(childRef,'childRef');
//   console.log(childRef.value.inputValue,'inputValue');
//   console.log(childRef.value.exposeMethod,'exposeMethod');
  
// },1000)

// provide传参方式
let titleProvide = shallowRef('aaa')
provide('titleProvide',titleProvide)
setTimeout(()=>{
  console.log(titleProvide,'000000');
  
  titleProvide.value ='我是provide的值'
},2000)
</script>