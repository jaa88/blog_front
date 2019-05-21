<template>
  <div>
    <h1>vuex 测试</h1>
  </div>
</template>

<script>
  import {getUserCount} from "../../api/api";

  export default {
      mounted(){
          this.getUserCountVue()
      },

      methods: {
          getUserCountVue(){
              getUserCount({}).then(res =>{
                  console.log("后台查询到的用户数："+res.data)
              })
          }
    }
  }

</script>