<template>
  <div id="app">
    <h3>Flight data</h3>
    <h4>Total number of flights: {{flights.length}}</h4>
    <h5>-includes {{businessClassFlights.length}} Business Class ({{((businessClassFlights.length / flights.length)*100).toFixed(0)}}%)</h5>
    <h4>There are {{departuresFromManchester.length}} departures from Manchester</h4>
    <!-- <flight-filter :flights="flights" :departureAirports="departureAirports" :departureDates="departureDates"/> -->
    <form  class="date">
        <label for="date-select">Filter by date:</label>

        <select id="date-select" v-model="depDate">
          <option value=null>--Please choose departure date--</option>
          <option v-for="date in departureDates" :value="date">{{date}}</option>
        </select>
    </form>

    <h4 v-if="filteredDeparturesFromManchester.length>0"> There are {{filteredDeparturesFromManchester.length}} flights from Manchester on {{depDate}}</h4>
  </div>
</template>

<script>

export default {
  data() {
    return {
      flights: [],
      businessClassFlights: [],
      departureAirports: [],
      departureDates: [],
      departuresFromManchester: [],
      filteredDeparturesFromManchester: [],
      depDate: null
    }
  },



  watch: {
    flights(newValue, oldValue) {
      this.listDepartureAirports();
      this.listDepartureDates();
      this.listBizClassFlights();
      this.listManchesterFlights();
    }
  },

  methods: {
    getFlights(){
      return fetch('http://localhost:3000/')
      .then(res => res.json())
      .then(data => this.flights = data)
      .then(data => this.filteredFlights = data)
    },

    //write method to get list of unique departure airports
    listDepartureAirports(){
      const airports = this.flights.map((flight) => {
        return flight["_attributes"].depair
      });
      const uniqueAirports = [...new Set(airports)]
      this.departureAirports = uniqueAirports
    },

    //function to list unique departure dates
    listDepartureDates(){
      const dates = this.flights.map((flight) => {

        return flight["_attributes"].outdepartdate
      });
      const uniqueDates = [...new Set(dates)]
      this.departureDates = uniqueDates
    },

    //function to get all business class flights
    listBizClassFlights(){
      const bizFlights = this.flights.filter((flight) => {
        return flight["_attributes"].outflightclass === "Business"
      });
        this.businessClassFlights = bizFlights
    },

    //function to get all Manchester departures
    listManchesterFlights(){
      const manchesterDepartures = this.flights.filter((flight) => {
        return flight["_attributes"].depair === "MAN"
      });
      this.departuresFromManchester = manchesterDepartures
    },

    // mapManchesterFlightsByDate(){
    //   const MANflightsMap = new Map();
    //   this.manchesterDepartures.filter((flight) => {
    //     const date = flight["_attributes"].outdepartdate;
    //     if (MANflightsMap[date] == null){
    //       MANflightsMap[date] = 1
    //     }
    //     else (MANflightsMap[date] += 1)
    //   });
    //   return MANflightsMap;
    // },

    // listManchesterFlightsByDate(){
    //   const MANFlightsOn = this.manchesterDepartures.filter((flight) => {
    //     flight["_attributes"].outdepartdate === ""
    //   });
    // },


  },

  mounted(){
    this.getFlights()

  },

  computed: {
    //Computed property should filter out flights for selected date
    MANflightsOnSelectedDate(){
      const flightsOn = this.departuresFromManchester.filter((flight) => {
        return flight["_attributes"].depair === this.depDate
      });
      this.filteredDeparturesFromManchester = flightsOn;
    }
  }

}

</script>
