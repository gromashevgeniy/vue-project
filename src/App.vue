<template>
  <body>
    <div class="wrapper">
      <h1> Weather app </h1>
      <p> Weather in {{ city == "" ? "your town" : cityName }}</p>
      <input type="text" v-model="city" placeholder="Entry your town">
      <button v-show="city != ''" @click="getWeather()">Show your weather</button>
      <p class="error">{{ error }}</p>
      <p>{{ info }}</p>
    </div>
  </body>
</template>

<script>
import axios from 'axios';

export default{
  data(){
    return{
      city: "",
      error: "",
      info: null,
    }
  },
  computed: {
    cityName(){
      return "\"" + this.city + "\"";
    }
  },
  methods: {
    getWeather(){
      if(this.city.trim().length < 2){
        this.error = "You should entry more then one symbol";
        return false;
      }
      this.error = '';

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=cb7a24eb1782e189e17cbf7e72840cd5`)
      .then(res => (this.info = res.data));
    }
  }
}
</script>

<style scoped>

.error{
  color: red;
}

.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background: black;
  color: white;
  text-align: center;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
  font-size: large;
}

.wrapper input {
  margin-top: 30px;
  background:transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: white;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
  text-align: center;
}

.wrapper input:focus{
  border-bottom-color: #6e2d7d;
}

.wrapper button{
  background: #e3bc4b;
  color: white;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}

</style>