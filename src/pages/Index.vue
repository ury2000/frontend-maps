<template>
  <q-page class="flex flex-block">
    <MapOSM></MapOSM>
  </q-page>
</template>

<script>
  import MapOSM from '../components/Map'

  export default {
    name: 'PageIndex',
    components: {MapOSM}
  }
</script>
