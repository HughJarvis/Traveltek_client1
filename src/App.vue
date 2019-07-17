<template>
  <div id="app">
    <h3>Flight data</h3>
    <h4>Total number of flights: {{flights.length}}</h4>
    <h5>-includes {{businessClassFlights.length}} Business Class ({{((businessClassFlights.length / flights.length)*100).toFixed(0)}}%)</h5>

    <flight-filter :flights="flights" :departureAirports="departureAirports" :departureDates="departureDates"/>

  </div>
</template>

<script>

import FlightFilter from '@/components/FlightFilter.vue';

export default {
  data() {
    return {
      flights: [],
      businessClassFlights: [],
      departureAirports: [],
      departureDates: [],
    
    }
  },


  components: {
    'flight-filter': FlightFilter
  },

  watch: {
    flights(newValue, oldValue) {
      this.listDepartureAirports();
      this.listDepartureDates();
      this.listBizClassFlights();

    }
  },

  methods: {
    getFlights(){
      return fetch('http://localhost:3000/')
      .then(res => res.json())
      .then(data => this.flights = data)
      .then(data => this.filteredFlights = data)
    },



    //write method to get all departure airports
    listDepartureAirports(){
      const airports = this.flights.map((flight) => {
        return flight["_attributes"].depair
      });
      const uniqueAirports = [...new Set(airports)]
      this.departureAirports = uniqueAirports
    },

    listDepartureDates(){
      const dates = this.flights.map((flight) => {

        return flight["_attributes"].outdepartdate
      });
      const uniqueDates = [...new Set(dates)]
      this.departureDates = uniqueDates
    },



    listFlightNumbers(){
      const flightNos = this.filteredFlights.map((flight) => {
        return flight["_attributes"].outflightno
      });
        return flightnos
    },

    listBizClassFlights(){
      const bizFlights = this.flights.filter((flight) => {
        return flight["_attributes"].outflightclass === "Business"
      });
        this.businessClassFlights = bizFlights
    }






    //write method to get flights from given airport on given date
  },

  mounted(){
    this.getFlights()

  },

  computed: {

  }

}

</script>
