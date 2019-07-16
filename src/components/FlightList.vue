<template lang="html">
  <div>
    <FlightListItem v-for="flight in flights" :flight="flight"/>
  </div>
</template>

<script>
import FlightListItem from '@/components/FlightListItem.vue';

export default {
  name: 'flight-list',
  props: ['flights'],
  components: { FlightListItem }
}
</script>

<style lang="css" scoped>
</style>
