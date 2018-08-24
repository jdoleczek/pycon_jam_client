<template>
  <div id="app">
    <div id="userinfo" v-if="!userinfo">
      <div class="box">
        <h2>Autoryzacja</h2>
        <i>Wpisz użytkownika by zalogować</i>
        <b-input-group>
          <b-form-input v-model="username" placeholder="username"></b-form-input>
          <b-input-group-append>
            <b-btn variant="outline-secondary" @click="authenticate">Login</b-btn>
          </b-input-group-append>
        </b-input-group>
      </div>
    </div>

    <div v-else class="container">
      <h1>{{userinfo.login}}</h1>
      <div v-for="val,stat in userinfo.stats">
        <strong>{{stat}}:</strong> {{val}}
      </div>
    </div>
  </div>
</template>

<script type="text/javascript">
export default {
  data () {
    return {
      username: 'user',
      userinfo: null
    }
  },
  methods: {
    authenticate () {
      this.axios.get('http://127.0.0.1:5000/userinfo', {headers: {Authentication: this.username}})
        .then(resp => {
          if (resp.status === 200) {
            this.userinfo = resp.data
          } else {
            this.username = ''
          }
        })
    }
  }
}
</script>

<style lang="scss">
#userinfo {
  display: block;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: #f8f8f8;

  &>.box {
    position: absolute;
    width: 460px;
    height: 200px;
    margin: auto;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    border-radius: 8px;
    background: #fff;
    box-shadow: 2px 2px 4px #eee;
    padding: 46px 36px;
  }
}
</style>
