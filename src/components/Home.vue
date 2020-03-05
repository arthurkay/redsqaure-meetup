<template>
  <div class="HomeComponent col-md-12">
      <div class="head">
          <h1> {{ heading }} </h1>
          <p> {{ msg }} </p>
      </div>
      <div class="col-md-12 body">
        <input type="hidden" v-model="showJoin" />
          <div class="row" id="join-room" v-if="showJoin">
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
            <RoomComponent  v-if="!showJoin"/>
          </div>
      </div>
  </div>
</template>

<script src=jvb_url></script>
<script>
import RoomComponent from '@/components/Room.vue'
export default {
  name: 'HomeComponent',
  components: {
    RoomComponent
  },
  props: {
    msg: String,
    heading: String
  },
  mounted () {
    const jitsi = document.createElement('script')
    jitsi.setAttribute('src', this.jvb_url)
    document.head.appendChild(jitsi)
  },
  data () {
    return {
      name: 'user' + Math.random(10).toString(36).substr(9),
      room: Math.random(10000).toString(36).substr(2),
      showJoin: true,
      jitsi_domain: process.env.VUE_APP_DOMAIN,
      jvb_url: process.env.VUE_APP_JVB_URL,
      appName: process.env.VUE_APP_NAME || 'RedSqaure MeetUp',
      provider: process.env.VUE_APP_PROVIDER || 'Arthur Kalikiti'
    }
  },
  methods: {
    hideShowJoinRoom () {
      if (this.showJoin) {
        this.showJoin = false
      }
      else {
        this.showJoin = true
      }
    },
    join (name, room) {
      let showJoin = this.showJoin
      this.hideShowJoinRoom()
      // Give DOM time to process
      let prom = new Promise((resolve, reject) => {
      if (this.showJoin !== showJoin) {
        resolve('success')
      }
      else {
        reject('failed')
      }
      })

      prom.then(result => {
        this.makeAPICall(name, room)
      }, err => {
        alert('Err '+err.message)
      })
    },
    makeAPICall(name, room) {
      const domain = this.jitsi_domain
      const options = {
        roomName: room,
        width: 1024,
        height: 590,
        parentNode: document.querySelector('#meet'),
        interfaceConfigOverwrite: {
          SHOW_JITSI_WATERMARK: false,
          APP_NAME: this.appName,
          NATIVE_APP_NAME: this.appName,
          PROVIDER_NAME: this.provider
        }
      }
      const vidApi = new JitsiMeetExternalAPI(domain, options)
      vidApi.executeCommand('toggleAudio', [])
      vidApi.executeCommand('toggleVideo', [])
      vidApi.executeCommand('displayName', name)
      vidApi.on('readyToClose', (evt) => {
        this.hideShowJoinRoom()
        // Possibly dipose room vidApi.dispose()
      })
    }
  },
  computed: {
    function () {
      return {
        // Nothing yet
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
