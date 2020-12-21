<template>
  <div id="wrapper">
    <component :is="selectedComponent"/>
  </div>
</template>

<script>
import Home from '~/components/home.vue'
export default {
   components:{
     'home': Home
   },
   data(){
     return{
       selectedComponent:'home'
     }
   }
}
</script>
<style
Home lang="scss" scoped>
#wrapper{
  width: 100vw;
  height: 100vh;
  overflow: auto;
}
</style>