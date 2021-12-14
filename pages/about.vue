
<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'AboutPage',

})
</script>

<template>
  <div>
    <p>Coder</p>
    <h1>


      <a-radio-group :value="120">
        <a-radio-button value="large"> Large </a-radio-button>
        <a-radio-button value="default"> Default </a-radio-button>
        <a-radio-button value="small"> Small </a-radio-button>
      </a-radio-group>
      <a-button type="primary" block> Primary </a-button>
    </h1>

  </div>
</template>

<style lang="scss" scoped>
h1 {
  color: red;
  p {
    color: blue;
  }
}
</style>
