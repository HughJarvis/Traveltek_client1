<template lang="html">
  <div>
    <FlightListItem v-for="flight in filteredFlights" :flight="flight"/>
  </div>
</template>

<script>
import FlightListItem from '@/components/FlightListItem.vue';

export default {
  name: 'flight-list',
  props: ['filteredFlights'],
  components: { FlightListItem }
}
</script>

<style lang="css" scoped>
</style>
