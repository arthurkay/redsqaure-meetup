<template>
  <div class="HomeComponent">
      <div class="head">
          <h1> {{ heading }} </h1>
          <br />
          <p> {{ msg }} </p>
      </div>
  </div>
</template>

<script>
export default {
  name: 'HomeComponent',
  props: {
    msg: String,
    heading: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
