<template lang="html">
  <div class="flight-list-item">
   <p>{{flight["-carrier"]}} {{flight["-outflightno"]}} from {{flight["-depair"]}} to {{flight["-destair"]}} on {{flight["-outdepartdate"]}}</p>
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
