<template>
  <q-page class="flex flex-center">
    <img
      alt="Quasar logo"
      src="~assets/quasar-logo-full.svg"
    >
    <div class="column">
      <div class="col-auto">
        <q-btn label="Check for updates" @click="check" />
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  methods: {
    check () {
      // const { app, autoUpdater, dialog } = require('electron').remote
      const { app, autoUpdater } = require('electron').remote
      const server = 'https://your-deployment-url.com'
      const url = `${server}/update/${process.platform}/${app.getVersion()}`
      autoUpdater.setFeedURL({ url })
      autoUpdater.checkForUpdates()

      autoUpdater.on('update-downloaded', (event, releaseNotes, releaseName) => {
        console.log('Update found!')
        console.log(releaseName)
      })

      autoUpdater.on('error', message => {
        console.error('Error!')
        console.error(message)
      })
    }
  }
}
</script>
