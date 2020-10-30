<template>
  <div id="app" class="container mt-5 md-5"> 
    <FormValidation/>
  </div>
</template>

<script>
import FormValidation from "./components/FormValidation"


export default {
  name: 'App',
  components: {
    FormValidation
  }
}
</script>

<style>
  #app {
    width: 600px;
    margin: 0 auto;
  } 
</style>
