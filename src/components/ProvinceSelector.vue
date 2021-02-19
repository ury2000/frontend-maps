<template>
  <div class="q-pa-md">
    <div class="q-gutter-md row">
      <q-select
        filled
        v-model="model"
        hide-selected
        use-input
        fill-input
        input-debounce="0"
        :options="options"
        @filter="filterFn"
        hint="filtro de provincias"
        placeholder="Selecccione"
        @input="searchProvinceFn"
      >
        <template v-slot:no-option>
          <q-item>
            <q-item-section class="text-grey">
              No results
            </q-item-section>
          </q-item>
        </template>
      </q-select>
    </div>
  </div>
</template>

<script>
  const provincesArr = [
    'Pinar del Río', 'Artemisa', 'La Habana', 'Matanzas', 'Cienfuegos', 'Villa Clara', 'Ciego de Ávila',
    'Camaguey', 'Las Tunas', 'Holguin', 'Guantánamo', 'Granma', 'Santiago de Cuba'
  ]

  export default {
    name: 'ProvinceSelector',
    data() {
      return {
        model: null,
        options: provincesArr
      }
    },

    methods: {
      filterFn(val, update, abort) {
        update(() => {
          const needle = val.toLowerCase();
          this.options = provincesArr.filter(v => v.toLowerCase().indexOf(needle) > -1)
        })
      },
      searchProvinceFn(value) {
        this.$root.$emit('getProvinceBoundary', value)
      }
    }
  }
</script>

<style scoped>

</style>
