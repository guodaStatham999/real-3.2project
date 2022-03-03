<template>
  <div class="hello">
      <h1>这个是组件孩子</h1>
      <h2>下面是父亲传递过来的列表</h2>
      <ul>
          <li v-for='item in props.list' style="display:block;">
              <span>我的名字{{item.name}}</span> +++ <span>我的年龄{{item.age}}</span>
          </li>
          <br>
      </ul>
      <input type="text" v-model="value" placeholder="请输入">
      <button @click="addToParent">增加到父级</button>
      <div>
         <div> key1:{{props.key1}}</div>
         <div> value2:{{props.value2}}</div>
      </div>
      <button @click="changeVModel">修改vmodel值到父级</button>
  </div>
</template>

<script lang="ts" setup>
    import {defineProps,ref,defineEmits } from 'vue'
    // 接受参数
    let props =  defineProps({
        list:{
            type:Array,
            default:()=>[]
        },
        key1:{
                 type:String,
            default:''
        },
        value2:{
                 type:String,
            default:''
        },
    })
    console.log(props);
    // 属性添加到父级
    let emits =defineEmits(['add','update:key1','update:value2'])
    let value = ref('')

    function addToParent(){
        emits('add',value.value)
        value.value = ''
    }

    function changeVModel(){
        emits("update:key1", "新的key1")
        emits("update:value2", "新的value")
    }
    
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
