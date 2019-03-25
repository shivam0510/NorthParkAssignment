<template>
  <form name="f" autocomplete="off">
    <div id="loginBlock">
      <div>
        <h1 class="loginHeading">Login</h1>
      </div>
      <div>
        <label for="login" id="username-label">
            <input autocapitalize="off" autocomplete="off" autocorrect="off" id="uname" name="j_username"
                  placeholder="Username" spellcheck="false" type="text" autofocus required="">
        </label>
        <label for="password" id="password-label">
            <input autocapitalize="off" autocomplete="off" autocorrect="off" id="password" name="j_password"
                  placeholder="Password" spellcheck="false" type="password" value="" required="">
        </label>
        
      </div>
      <input id="login-button" type="button" value="Sign In" name="_eventId_proceed" 
                  v-on:click="authLogin(posts)">
        
    </div>
  </form>
</template>

<script>
import axios from 'axios'

export default {

methods:{
    //method to authorise login
    authLogin(posts){
      var uname = document.getElementById("uname").value;
      var pass = document.getElementById("password").value;
      var flag = false;
      for(var i=0; i<posts.length;i++){
        if(posts[i].id === uname){
          flag = true;
          if(posts[i].password == pass){
            this.$router.push({path: '/dashbord'});
            break;
          }else{
            flag = false;
            break;
          }
        }
      }
      if(!flag){
        alert('invalid username or password');
      }
  }
},

data() {
    return {
      posts: [],
      errors: [],
    }
  },

  // Fetches posts when the component is created.
  created() {
    axios.get('../User.json')
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    });
  }
}
</script>

<style>

.loginHeading {
  font: 28px/1.1 Georgia,serif;
    color: #000;
    padding: 18px 0 0;
    margin: 20px 0;
    border-bottom: 1px solid black;
    padding-bottom: 20px;
}

div {
  display : block;
}

#loginBlock {
  width: 380px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin: -200px 0 0 -140px;
  font-size: larger;
}

input {
  width: 100%;
}
</style>

