<template>
  <q-header elevated class="bg-primary q-pa-xs">
    <q-toolbar>
      <q-toolbar-title>
        <span class="text-h4 q-mr-md text-weight-bold"><q-icon name="menu" class="q-pb-xs"/> Cooperación</span>
        <span class="ext-subtitle1">UE-Cuba</span>
      </q-toolbar-title>
      <!--        <q-toolbar-title>-->
      <!--          {{ $t('projectsMap') }}-->
      <!--        </q-toolbar-title>-->

      <div class="row items-center">
        <div class="col">
          <label class="text-weight-bold"> Diagramas de Cooperación</label>
        </div>
        <div class="col-4 cursor-pointer">
          <span>ODS <q-icon name="info"></q-icon> </span>
        </div>
        <div class="col-4">
          <q-select
            v-model="lang"
            :options="langOptions"
            dense
            borderless
            emit-value
            map-options
            options-dense
            style="min-width: 100px;"
            class="q-pa-xs my-text-white"
          />
        </div>
      </div>
    </q-toolbar>
  </q-header>
</template>
<script>
  export default {
    name: 'my-header',
    data() {
      return {
        lang: this.$i18n.locale,
        langOptions: [
          {value: 'en-us', label: 'English'},
          {value: 'es-es', label: 'Español'}
        ]
      }
    },
    watch: {
      lang(lang) {
        this.$i18n.locale = lang
      }
    }
  }
</script>
<style >
   .my-text-white.q-select .q-field__append, .my-text-white.q-select span{
    color: white !important;
  }
</style>
