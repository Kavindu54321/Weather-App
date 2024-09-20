<template>
  <q-page class="flex column" style="background: linear-gradient(to right, #000046, #1cb5e0);">
    <div class="col q-pt-lg q-px-md">
       <q-input  
       v-model="search" 
      placeholder="Search" 
      dark
      borderless
       >
        <template v-slot:before>
          <q-icon
          @Click="getLocation" 
          name="my_location" />
        </template>

       

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>

    <template v-if="weatherDate">
       <div class="col text-white text-center">
      <div class="text-h4 text-weight-light">
        Sri Lanka
      </div>
      <div class="text-h6 text-weight-light">
        Rain
      </div>
      <div class="text-h1 text-weight-thin q-my-lg relative-position">
        <span>8</span>
        <span class="text-h4 relation-position degree">&deg;</span>
        
      </div>
    </div>

    <div class="col text-center">
      <img src="https://www.fillmurray.com/100/100" alt="Bill">
    </div>
    </template>

    <template v-else>
      <div class="col column text-center text-white">
        <div class="col text-h2 twxt-weight-thin">
          Quaser <br>Weather
        </div>
          <q-btn 
          @Click="getLocation"
          class="col"
           flat>
          <q-icon left size="3em" name="my_location" />
          <div>Find My Location</div>
        </q-btn>
      </div>
    </template>

    <div class="col skyline">

    </div>

    
  </q-page>
</template>

<script setup>

  defineOptions({
  name: 'IndexPage',
  date(){
    return {
      search:'',
      weatherDate: null,
      lat:null,
      lon:null,
      apiUrl:'https://samples.openweathermap.org/data/2.5/weather',
      apiKey:'dc68df57f2870e29dc26dcfd9cf38885'
    }
  },
  methods:{
    getLocation(){
      navigator.geolocation.getCurrentPosition(position => {
        console.log('position:', position);
        this.lat = position.coords.latitude
        this.lon = position.coords.longitude
        this.getWeatherByCoords()
      })
    },
    getWeatherByCoords(){
      this.$axios('${this.apiUrl}?lat=${this.lat}&lon=${this.lon}&appid=${this.apiKey}&units=metric')
      .then(response=>{
        this.weatherDate = response.data
        
      })
      
    }
  }
});
</script>


<style scoped>
 .q-page{
  background: linear-gradient(to right, #000046, #1cb5e0);
 }
  .degree {
  top: -40px;
  position: relative;
}
 .skyline {
  flex:0 0 100px;
  background:url(new.png);
  background-size: contain;
  background-position: center bottom;
 }
</style>




