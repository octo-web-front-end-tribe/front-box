<template>
  <ul v-if="devices && devices.length">
    <li v-for="device of devices">
      <p><strong>{{device.location}}</strong></p>
      <p>{{device.presence}}</p>
      <p>{{device.since}}</p>
    </li>
  </ul>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      devices: [],
      errors: []
    }
  },

  // Fetches posts when the component is created.
  created () {
    axios.get(`http://localhost:3000/devices`)
      .then(response => {
      // JSON responses are automatically parsed.
        this.devices = response.data
      })
      .catch(e => {
        this.errors.push(e)
      })

    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
  }
}
</script>
