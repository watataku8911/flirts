<template>
  <div id="app">
    <div class="opning" v-show="show">
      <img src="@/assets/logo.jpg">
    </div>
    <div v-show="!show">
      <Appheader></Appheader>
      <div class="module--spacing"></div>
      <main>
        <HelloWorld />
      </main>
      <Appfooter></Appfooter>
    </div>
  </div>
</template>

<script>
import Appheader from './components/Appheader'

import Appfooter from './components/Appfooter'
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    Appheader,
    Appfooter,
    HelloWorld
  },
  data() {
    return {
      show: true
    }
  },
  mounted() {
    setTimeout(() => {
      this.show = false
    }, 2500);
  }
}
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.opning {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateY(-50%) translateX(-50%);
  -webkit-transform: translateY(-50%) translateX(-50%);
}

.opning img {
  max-width: 100%;
}

.module--spacing {
  height: 50px;
}
</style>
