<template lang="html">
  <div class="filter">
<form class="airport">
  <label for="departure-select">Show flights from:</label>

  <select id="departure-select" v-model="depAirport">
    <option value=null>--Please choose departure airport--</option>
    <option v-for="airport in departureAirports" :value="airport">{{airport}}</option>
  </select>
  <button>Filter</button>
</form>

<form class="date">
    <label for="date-select">Select departure date:</label>

    <select id="date-select" v-model="depDate">
      <option value=null>--Please choose an option--</option>
      <option v-for="date in departureDates" :value="date">{{date}}</option>
    </select>
    <button>Filter</button>
</form>
<flight-list v-if="depAirport" :filteredFlights="filteredFlights"/>
  </div>
</template>

<script>
import FlightList from '@/components/FlightList.vue';

export default {
  data(){
    return {
      depAirport: null,
      depDate: null,
      filteredFlights: [],
    }
  },

  name: 'flight-filter',
  props: ["flights", "departureAirports", "departureDates"],

  components: {
    'flight-list': FlightList
  },

  methods: {

    listFlightsFromManchester(){
      const manchesterFlights = this.flights.filter((flight) => {
        return flight["_attributes"].depair === "MAN"
      });
      this.flightsFromMAN = manchesterFlights
    }
  },

  computed: {
    //write method to get flights departing given airport
    flightsFromSelectedAirport(){
      const flightsFrom = this.flights.filter((flight) => {
        return flight["_attributes"].depair === depAirport;
      });
      this.filteredFlights = flightsFrom;
    },

    //write method to get flights on given date
    flightsOn(depDate){
      const flightsOn = this.filteredFlights.filter((flight) => {
        flight["_attributes"].outdepartdate === depDate;
      })
      this.filteredFlights = flightsOn;
    },

  }
}
</script>

<style lang="css" scoped>
</style>
