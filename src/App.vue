<template>
  <div id="app">

    <h1>Flight data</h1>
  </div>
</template>

<script>

export default {
  data() {
    return {
      flights: []
    }
  },

  methods: {
    getFlights(){
      return fetch('http://localhost:3000/')
      .then(res => res.json())
      .then(flights => this.flights = flights)
    }
  },
  mounted(){
    this.getFlights()
  },

  computed: {
    
  }

}
</script>
