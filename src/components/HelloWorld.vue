<template>
  <div class="hello">
    <button @click="fd">测试防抖</button>
    <p>防抖：每次触发都会重新计算定时器，最终只执行一次</p>
    <button @click="jl">测试节流</button>
    <p>节流：间隔固定时间执行一次</p>
  </div>
</template>

<script>
import { ref ,defineComponent} from "vue";

export default defineComponent ({
  setup() {
    // 防抖函數
    let ftimer = null;
    const fd = () => {
      clearTimeout(ftimer);
      ftimer = setTimeout(() => {
        console.log("FD success !");
      }, 1000);
    };
    //节流函数
    let jtimer = ref(null);
    let canRun = true;
    const jl = () => {
      if (!canRun) {
        return;
      }
      canRun = false;
      jtimer.value = setTimeout(() => {
       console.log("JL success !")
        canRun = true;
      }, 1000);
    };

    let newP = new Promise((resolve,reject)=>{
      console.log("0000000")
      // 做一些异步操作
      setTimeout(()=>{
        resolve("成功了");
      },100)
      reject("fail")
      newP();
    })
    return {
      fd,
      jl,
    };
  },
})
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
