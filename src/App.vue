<template>
  <div id="app">
    <h3>Flight data</h3>
    <flight-filter/>
    <h4>Total flights: {{flights.length}}</h4>
    <flight-list :flights="flights"/>
  </div>
</template>

<script>
import FlightList from '@/components/FlightList.vue';
import FlightFilter from '@/components/FlightFilter.vue';

export default {
  data() {
    return {
      flights: [],
      filteredFlights: []
    }
  },

  components: {
    'flight-filter': FlightFilter,
    'flight-list': FlightList
  },

  methods: {
    getFlights(){
      return fetch('http://localhost:3000/')
      .then(res => res.json())
      .then(data => this.flights = data)
    },

    //write method to get flights departing given airport
    flightsFrom(airport){
      const flightsFrom = this.flights.filter((flight) => {
        flight["-depair"] === airport.JSON.stringify;
      });
      return flightsFrom;
    },

    //write method to get flights on given date
    flightsOn(date){
      const flightsOn = this.flights.filter((flight) => {
        flight["-outdepartdate"] === date.JSON.stringify;
      })
      return flightsOn;
    },

    //write method to get all departure airports
    listDepartureAirports(){
      const results = [...new Set(flights.map(flight => flight["-depair"]))]
      return results;
    }


    //write method to get flights from given airport on given date
  },

  mounted(){
    this.getFlights()

  }
}

</script>
