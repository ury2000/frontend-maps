<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title>
          Cooperación UE-Cuba
        </q-toolbar-title>
        <q-space/>
        <q-toolbar-title>
          {{ $t('projectsMap') }}
        </q-toolbar-title>
        <q-space/>
        <q-select
          v-model="lang"
          :options="langOptions"
          dense
          borderless
          emit-value
          map-options
          options-dense
          style="min-width: 100px"
        />
      </q-toolbar>
    </q-header>
    <q-page-container>
      <router-view />
    </q-page-container>
    <q-footer elevated class="bg-grey-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          FOOTER
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
  export default {
    name: 'MainLayout',
    components: { },
    data () {
      return {
        lang: this.$i18n.locale,
        langOptions: [
          { value: 'en-us', label: 'English' },
          { value: 'es-es', label: 'Español' }
        ]
      }
    },
    watch: {
      lang (lang) {
        this.$i18n.locale = lang
      }
    }
  }
</script>
