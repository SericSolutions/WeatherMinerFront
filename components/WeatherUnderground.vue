<template>
  <v-expansion-panel>
    <v-expansion-panel-content key = "1">
      <div slot="header">{{data.current_observation.observation_time_rfc822}}</div>
      <v-card>
        <table class="table">
          <thead>
          <tr>
            <th class="apa">Key</th>
            <th class="apa">Value</th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(value, key) in flattenObject(data.current_observation)">
            <td> {{key}} </td>
            <td> {{value}} </td>
          </tr>
          <tr v-for="(value, key) in data.forecast.simpleforecast.forecastday">
            <td> Day {{key +1}} forecast </td>
            <td>
              <v-dialog v-model="dialog" width="550" scrollable>
                <v-btn slot="activator" color="red lighten-2" dark >
                  Click Here
                </v-btn>

                <v-card>
                  <v-card-title class="headline grey lighten-2 text-center" primary-title>
                    Day {{key + 1}} forecast
                  </v-card-title>

                  <v-card-text>
                    <table class="table">
                      <thead>
                      <tr>
                        <th class="apa">Key</th>
                        <th class="apa">Value</th>
                      </tr>
                      </thead>
                      <tbody>
                      <tr v-for="(value, key) in flattenObject(value)">
                        <td> {{key}} </td>
                        <td> {{value}} </td>
                      </tr>
                      </tbody>
                    </table>
                  </v-card-text>
                  <v-divider></v-divider>
                </v-card>
              </v-dialog>
            </td>
          </tr>
          </tbody>
        </table>
      </v-card>
    </v-expansion-panel-content>
  </v-expansion-panel>
</template>

<script>
  export default {
    data () {
      return {
      }
    },
    props: ['data'],
    beforeMount () {
    },
    methods: {
      flattenObject (ob) {
        var toReturn = {}
        for (var i in ob) {
          if (!ob.hasOwnProperty(i)) continue

          if ((typeof ob[i]) === 'object') {
            var flatObject = this.flattenObject(ob[i])
            for (var x in flatObject) {
              if (!flatObject.hasOwnProperty(x)) continue

              toReturn[i + '.' + x] = flatObject[x]
            }
          } else {
            toReturn[i] = ob[i]
          }
        }
        return toReturn
      }
    }
  }
</script>