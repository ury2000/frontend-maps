<template>
  <div class="q-pa-md full-width">
    <q-card class="my-card">
      <q-toolbar>
        <div class="text-h6">{{ $t('projectsMap') }}</div>
        <q-space></q-space>
        <q-select style="max-width: 200px"
                  v-model="model"
                  hide-selected
                  use-input
                  fill-input
                  input-debounce="0"
                  :options="options"
                  @filter="filterFn"
                  :placeholder="$t('provinceFilter')"
                  @input="updateGeoJson"
        >
          <template v-slot:no-option>
            <q-item>
              <q-item-section class="text-grey">
                No results
              </q-item-section>
            </q-item>
          </template>
          <template v-slot:append>
            <q-icon name="search"/>
          </template>
        </q-select>
      </q-toolbar>
      <l-map style="min-height:420px" :zoom="zoom" :center="center">
        <l-tile-layer :url="url"></l-tile-layer>
        <l-geo-json :geojson="geojson"></l-geo-json>
        <l-control position="bottomright">
          <table style="border: 1px solid
          red;background: #f5f5f5" cellspacing="10">
            <tr>
              <td><b>Proyectos 50</b></td>
              <td><b>Financiación 70 000 000€</b></td>
            </tr>
          </table>
        </l-control>

      </l-map>
    </q-card>
  </div>
</template>

<script>
  import {LMap, LTileLayer, LGeoJson, LControl} from 'vue2-leaflet'
  import 'leaflet/dist/leaflet.css'

  const provincesArr = [
    'Pinar del Río', 'Artemisa', 'La Habana', 'Matanzas', 'Cienfuegos', 'Villa Clara', 'Ciego de Ávila',
    'Camaguey', 'Las Tunas', 'Holguin', 'Guantánamo', 'Granma', 'Santiago de Cuba', 'Isla de la Juventud'
  ]

  export default {
    components: {
      LMap,
      LTileLayer,
      LGeoJson,
      LControl
    },
    data() {
      return {
        url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
        zoom: 7,
        center: [21.783306, -79.643556],
        geojson: null,
        model: null,
        options: provincesArr
      }
    },
    methods: {
      async updateGeoJson(province) {
        // se usa "https://nominatim.openstreetmap.org" api
        let url = 'https://nominatim.openstreetmap.org/search.php?q=' + province + '&polygon_geojson=1&format=jsonv2';
        fetch(encodeURI(url))
          .then(response => response.json())
          .then(data => {
            data.sort((a, b) => (a['place_rank'] > b['place_rank'] ? 1 : -1));
            this.geojson = data[0].geojson
          })
      },
      filterFn(val, update, abort) {
        update(() => {
          const needle = val.toLowerCase();
          this.options = provincesArr.filter(v => v.toLowerCase().indexOf(needle) > -1)
        })
      },
    }
  }
</script>
