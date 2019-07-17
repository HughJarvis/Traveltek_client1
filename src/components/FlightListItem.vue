<template lang="html">
  <div class="flight-list-item">
   <p>{{flight["_attributes"].carrier}} {{flight["_attributes"].outflightno}} from {{flight["_attributes"].depair}} to {{flight["_attributes"].destair}} on {{flight["_attributes"].outdepartdate}}</p>
 </div>
</template>

<script>
export default {
  name: 'flight-list-item',
  props: ['flight']
}
</script>

<style lang="css" scoped>
p {
  font-size: 10px;
}
</style>
