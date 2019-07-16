<template>
  <div id="app">
    <h3>Flight data</h3>
    <flight-filter :flights="flights" :departureAirports="departureAirports" :departureDates="departureDates"/>
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
      filteredFlights: [],
      departureAirports: [],
      departureDates: []
    }
  },



  components: {
    'flight-filter': FlightFilter,
    'flight-list': FlightList
  },

  watch: {
    flights(newValue, oldValue) {
      console.log("new value: ", newValue);
      console.log("old value: ", oldValue);
    }
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

    listDepartureAirports: function(){
      const airports = [...new Set(flights.map(flight => {
        flight["-depair"]
      }))];
      this.departureAirports = airports
    },

    listDepartureDates: function(){
      const dates = [...new Set(flights.map((flight) => {
        flight["-outdepartdate"]
      }))];
      this.departureDates = dates
    }

    //write method to get all departure airports



    //write method to get flights from given airport on given date
  },

  mounted(){
    this.getFlights()

  },

  computed: {

  }

}

</script>
