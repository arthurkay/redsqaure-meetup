<template>
  <div class="home">
    <!--// img alt="Vue logo" src="../assets/logo.png"> //-->
    <HomeComponent
      heading="RedSqaure Meetup"
      msg="RedSqaure MeetUp | Online MeetUps"
    />
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
