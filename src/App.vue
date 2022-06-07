<template>
  <div class="app">
    <div v-if ="state.account.mid">Hello {{ state.account.memberName}}</div>
    <div v-else>
      <label for="loginId">
        <span>Id</span>
        <input type="text" id="loginId" v-model="state.form.loginId"/>
      </label>
      <label for="loginPw">
        <span>Password</span>
        <input type="password" id="loginPw" v-model="state.form.loginPw"/>
      </label>
      <hr />
      <button @click="submit()">LogIn</button>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import {reactive} from "vue";
export default {
  setup() {
    const state = reactive({
      account:{
      mid:null,
      memberName:""
      },
       form:{
         loginId:"",
         loginPw:""
       },
      const submit =()=>{
        const args={
          loginId=state.form.loginId,
          loginPw=state.form.loginPw,
        }
        
        axios.post("/api/account",args).then((res)=>{
          console.log(res);
        });
        
      }
    });

    axios.get("/api/account").then((res)=>{
      state.account= res.data;
    });

    return {state, submit};
  },
}
</script>
