<template lang="html">
  <div class="filter">
    <label for="departure-select">Choose departure airport:</label>

<select id="departure-select">
    <option value="">--Please choose an option--</option>
    <option v-for="airport in departureAirports" >{{airport}}</option>
</select>
  </div>
</template>

<script>
export default {
  name: 'flight-filter',
  props: ["flights", "departureAirports", "departureDates"]
}
</script>

<style lang="css" scoped>
</style>
