<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-8 col-md-offset-2">
          <logo/>
          <transition>
            <router-view></router-view>
          </transition>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import Logo from './components/logo.vue'

export default {
  name: 'app',
  data () {
    return {
    }
  },
  components: {
    Logo,
   
  },
  mounted:function(){
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
