<template>
  <q-layout view="hhh LpR fFf" class="red">
    <my-header :lang="lang" :lang-options="langOptions"/>

    <q-page-container>
      <router-view/>
    </q-page-container>
    <MyFooter/>
  </q-layout>
</template>

<script>
  import MyHeader from "./MyHeader";
  import MyFooter from "./MyFooter";

  export default {
    name: 'MainLayout',
    components: {MyFooter, MyHeader},
    data() {
      return {
      }
    }
  }
</script>

