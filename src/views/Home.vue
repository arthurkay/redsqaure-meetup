<template>
  <div class="home">
    <!--// img alt="Vue logo" src="../assets/logo.png"> //-->
    <div class="container">
      <div class="row">
        <HomeComponent
          heading="Living Open Source meetapp"
          msg="Online Training | Online MeetUps | Online Conferencing"
        />
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeComponent from '@/components/Home.vue'

export default {
  name: 'Home',
  components: {
    HomeComponent
  }
}
</script>
