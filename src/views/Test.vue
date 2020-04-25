<template>
  <div class="test">
    <h1>vue3.0 初体验</h1>
    <div class="user">
      <img src="https://user-gold-cdn.xitu.io/2020/4/22/1719f4f758a3a6d5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1" />
       <h2>前端劝退师 警告</h2>
    </div>
    <p>少年你的头发可还好，？？？？ 哈哈哈哈哈</p>
    <div>count: {{count}}</div>
    <div>count * 2 = {{doubleCount}}</div>
    <div>state from vuex {{a}}</div>
    <div class="btn">
      <button @click="add">add</button>
      <button @click="update">update a</button>
    </div>
   
  </div>
</template>

<script>
import { ref, computed, watch, getCurrentInstance } from 'vue'
 export default {
    setup () {
      const { ctx } = getCurrentInstance()
      //然后通过 ctx 属性获得当前上下文 获取路由信息
      console.log(ctx.$router.currentRoute.value)
      const count = ref(0)
      /**
       * 数量++
       */
      const add = () => {
        count.value++
      }
      watch(() => count.value, val => {
        console.log(`count is ${val}`)
      })
      const doubleCount = computed(() => count.value * 2)
      // 计算store的值
      const a = computed(() => ctx.$store.state.test.a)
      /**
       * 更新store 状态
       */
      const update = () => {
        ctx.$store.commit('setTestA', count)
      }
      return {
        count,
        doubleCount,
        add,
        a,
        update
      }
    }
 }
</script>
 
<style lang="scss" scoped>
.test {
  color:rebeccapurple
}
h2 {
  color: palevioletred;
}
div{margin-bottom: 15px;}
.user {
  width: 600px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  img{
    width: 300px;
    margin-right: 15px;
  }
}
.btn {
  width: 250px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  button {
    padding: 10px;
    background: red;
    font-size: 15px;
    color:#fff;
  }
}
</style>