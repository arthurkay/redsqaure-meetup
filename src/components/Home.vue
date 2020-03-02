<template>
  <div class="HomeComponent col-md-12">
      <div class="head">
          <h1> {{ heading }} </h1>
          <p> {{ msg }} </p>
      </div>
      <div class="col-md-12 body">
        <input type="hidden" v-model="showJoin" />
          <div class="row" id="join-room" v-if="showJoin == true">
            <div class="col-md-4">
              <div class="form-group">
                <label for="name">
                </label>
                <input type="text" name="name" id="name"
                  placeholder="name" v-model="name"/>
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group">
                <label for="room">
                </label>
                <input type="text" name="room" id="room"
                  placeholder="room" v-model="room" />
              </div>
            </div>
            <div class="col-md-4">
              <div class="form-group">
                <label for="submit">
                </label>
                <input type="button" name="submit" id="submit"
                  value="SUBMIT" class="btn btn-danger" v-on:click="join( name, room )"/>
              </div>
            </div>
          </div>
          <div class="row">
            <div id="meet">
            </div>
          </div>
      </div>
  </div>
</template>

<script src='https://meet.jit.si/external_api.js'></script>
<script>
export default {
  name: 'HomeComponent',
  props: {
    msg: String,
    heading: String
  },
  mounted () {
    const jitsi = document.createElement('script')
    jitsi.setAttribute('src', 'https://meet.jit.si/external_api.js')
    document.head.appendChild(jitsi)
  },
  data () {
    return {
      name: 'user' + Math.random(10).toString(36).substr(9),
      room: Math.random(10000).toString(36).substr(2),
      showJoin: true
    }
  },
  methods: {
     hideShowJoinRoom () {
      if (this.showJoin) {
        this.showJoin = false
        console.log(this.showJoin)
      }
      else {
        this.showJoin = true
        console.log(this.showJoin)
      }
    },
    join (name, room) {
      const domain = 'meet.jit.si'
      const options = {
        roomName: room,
        width: 700,
        height: 700,
        parentNode: document.querySelector('#meet')
      }
      const vidApi = new JitsiMeetExternalAPI(domain, options)
      vidApi.executeCommand('toggleAudio', [])
      vidApi.executeCommand('toggleVideo', [])
      vidApi.executeCommand('displayName', name)
      vidApi.on('readyToClose', (evt) => {
        this.hideShowJoinRoom()
        //document.querySelector("#meet").style.display = 'none';
        // Possibly dipose room vidApi.dispose()
      })
      this.hideShowJoinRoom()
      //document.querySelector("#meet").style.display = 'block';
    }
  },
  computed: {
    function () {
      //console.log(showJoin)
      return {
        //
      }
    }
  }
}
</script>

<style scoped>
#name {
  border: none;
  border-bottom: 1px solid red;
}
#room {
  border: none;
  border-bottom: 1px solid red;
}
.body {
  padding-top: 200px;
}
</style>
