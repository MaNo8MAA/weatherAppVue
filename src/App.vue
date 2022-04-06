<script >
export default {
  name: 'app',
  data(){
    return {
     api_key: 'c20fbdf454dfa626b2e9ada3a6b23241',
     url_base:'http://api.openweathermap.org/data/2.5/',
     query:'',
     weather:{}
    }
  },
  methods: {
    fetchWeather(e){
      if(e.key=="Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then((res) => {
          return res.json();
          
        }).then(this.setResults);
          
        }

      },
      setResults (results){
        this.weather = results;
      },
      dateBuilder(){
        let d =new Date();
        let months =['January', 'Febraury', 'March', 'Abril', 'May','June', 'July','August', 'September', 'October', 'November', 'December'];
        let days =["Sunday", "Monday", "Tuesday", "Wednsday", "Thursday", "Friaday", "Saturday"];
        
        let day = days[d.getDay()];
        let date =d.getDate();
        let month = months[d.getMonth()];
        let year = d.getFullYear();
        return `${day} ${date} ${month} ${year}`

  }
  }


}  
  

</script>

<template>
<div id="app" :class="typeof weather.main!='undefined' && weather.main.temp> 16 ? 'warm': ''">
 <main>
   <div class="search-box">
     <input type="text"
            class="search-bar" 
            placeholder="search..."
            v-model="query"
            @keypress="fetchWeather">
            
     <div class="test" id="yes"></div>
   </div>
   <div class="weather-wrap" v-if="typeof weather.main !='undefined'">
     <div class="location-box">
       <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
       <div class="date"> {{ dateBuilder() }}</div>
     </div>

     <div class="weather-box">
       <div class="temp">{{Math.round(weather.main.temp)}} C</div>
       <div class="weather">{{weather.weather[0].main}}</div>
     </div>
   </div>
 </main>
</div>

</template>

<style>
* {
  margin:0;
  padding:0;
  box-sizing: border-box;
}

body {
font-family: sans-serif;
}
#app{
  background-image: url(./assets/images.jpg);
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;

}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.76));
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
  .search-box .search-bar {
    display: block;
    width:100%;
    padding: 15px;
    color:#313131;
    font-size: 28px;
    
    appearance: none;
    border:none;
    outline: none;
    background: none;
   box-shadow: 8px 0 8px rgba(0,0,0,0.25);
    background-color:rgba(255, 255, 255, 0.3);
    border-radius: 0 16px 0 16px;
    transition: 0.4s;


  }
  .search-box .search-bar:focus {
      box-shadow: 8px 0 16px rgba(0,0,0,0.25);
      background-color:rgba(250, 244, 244, 0.75);
      border-radius: 16px 0 16px 0;
  }

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.location-box .date {
   color: #fff;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding:10px 25px;
  color:#fff;
  font-size: 125px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(0,0,0,0.25);
  border-radius: 16px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0,0,0,0.25);
}
.weather-box .weather {
  color:#fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  
}
#app.warm {
  background-image: url(./assets/warm.jpg);
}
</style>
