<template>
  <div>
  <v-layout
    row
    wrap
  >
    <v-flex
      xs4
    >
      <v-card class="mx-auto" max-width="344">
        <v-card-title primary-title>
          <div>
            <div>Total Positif</div>
          </div>
        </v-card-title>
        <v-card-text>
          <p class="display-1 text--primary">
            {{ totalConfirmed }}
          </p>
        </v-card-text>
      </v-card>
  
    </v-flex>

    <v-flex
      xs4
    >
      <v-card class="mx-auto" max-width="344">
        <v-card-title primary-title>
          <div>
            <div>Total Sembuh</div>
          </div>
        </v-card-title>
        <v-card-text>
          <p class="display-1 text--primary">
            {{ totalRecovered }}
          </p>
        </v-card-text>
      </v-card>
    
    </v-flex>

    <v-flex
      xs4
    >
      <v-card class="mx-auto" max-width="344">
        <v-card-title primary-title>
          <div>
            <div>Total Kematian</div>
          </div>
        </v-card-title>
        <v-card-text>
          <p class="display-1 text--primary">
            {{ totalDeaths }}
          </p>
        </v-card-text>
      </v-card>
    
    </v-flex>
  </v-layout>
  <uasoft-spacer/>
  <v-layout row wrap>
    <v-flex xs12>
      <v-data-table
        :headers="headers"
        :items="countries"
        class="elevation-1"
      ></v-data-table>
    </v-flex>

  </v-layout>
  </div>

</template>

<script>
import UasoftSpacer from '~/components/UasoftSpacer'

export default {
  components: {
    UasoftSpacer
  },
  data() {
    return {
      totalConfirmed: 0,
      totalRecovered: 0,
      totalDeaths: 0,
      countries: [],
      headers: [
          {
            text: 'Negara',
            value: 'Country'
          },
          { text: 'Positif terbaru', value: 'NewConfirmed' },
          { text: 'Total positif', value: 'Total Confirmed' },
          { text: 'Sembuh terbaru', value: 'NewRecovered' },
          { text: 'Total sembuh', value: 'TotalRecovered' },
          { text: 'Kematian terbaru', value: 'NewDeaths' },
          { text: 'Total kematian', value: 'TotalDeaths' }
        ]
    }
  },
  mounted() {
    this.getSummary()
  },
  methods: {
    getSummary() {
      this.$axios.get('https://api.covid19api.com/summary').then((response) => {
        
        this.totalConfirmed = response.data.Global.TotalConfirmed
        this.totalRecovered = response.data.Global.TotalRecovered
        this.totalDeaths = response.data.Global.TotalDeaths
        this.countries = response.data.Countries
      }, (error) => {
        console.log(error)
      })
    }
  }
}
</script>
