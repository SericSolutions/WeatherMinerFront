<template>
  <div></div>
</template>


<style>
  .apa {
    font-size: 25px !important;
    text-align: center;
  }
</style>

<script>
  import WeatherUnderground from '~/components/WeatherUnderground.vue'
  import DarkSky from '~/components/DarkSky.vue'
  import Firebase from 'firebase'

  export default {
    components: {
      'weather-underground': WeatherUnderground,
      'dark-sky': DarkSky
    },
    data () {
      return {
        data: null,
        gotData: false
      }
    },
    beforeMount () {
      console.log('beforeMount started')

      let config = {
        apiKey: 'AIzaSyA3PuZMq3iNNw8lveLJoB9qHF4mFdWgDuQ',
        authDomain: 'weatherminer.firebaseapp.com',
        databaseURL: 'https://weatherminer.firebaseio.com/',
        projectId: 'weatherminer',
        storageBucket: 'weatherminer.appspot.com',
        messagingSenderId: 'NO_ID'
      }

      let firebaseApp = Firebase.initializeApp(config)
      let db = firebaseApp.database()
      let darkSkyRef = db.ref('weatherminer/DarkSky')
      // let WeatherUndergroundRef = db.ref('WeatherUnderground')

      darkSkyRef.on('value', snapshot => {
        console.log(snapshot)
      }, (errorObject) => {
        console.log('The read failed: ' + errorObject.code)
      })
    },
    methods: {
    }
  }
</script>