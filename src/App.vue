<template>
 <div class="main" style="font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; z-index:-2">
   <section>
    
    <div class="input" >
      <input type="text" placeholder="Search" v-model="query" @keypress.enter="get()">
      <h1>{{weather.name}},{{weather.sys.country}}</h1>
      <p>{{date()}}</p>
      <div class="deg">
          <p style="font-size:58px">{{Math.round(weather.main.temp)}}°c</p>
          <h1 style="font-size: 50px;">{{ weather.weather[0].main}}</h1>
      </div>
    </div>
     <div class="maindiv">
      <img :src=" '/img/'+pic+'.jpg'">
     </div>
   </section>

 </div>

</template>
<!-- css part -->
<style>
.main{
  background-image: url("tree1.jpg");
  background-size: cover;
  background-repeat:repeat;
}
.section1{
 background: black
}
.deg h1{
    font-family: system-ui;
    margin-top: 30px;
    text-align: center;
    padding-right: 10px;
    position: absolute;
    left: -10%;
}
.deg p {
    border-radius: 50px 0px;
    text-shadow: 2px 2px #310112;
    background: #ffffff7a;
    padding: 15px;
    margin-top: 10px;
    text-align: center;

}
.deg{
  position: absolute;
  width: 140px;
  left:43%;
  display: block;
}

.input p {
    font-style: italic;
    font-size: 20px;
}
.input h1,p{
   font-family: 'Avenir', Helvetica, Arial, sans-serif;
    color: white;
    position: relative;
    top: 50px;
    font-size: 30px;
    text-shadow: 3px 1px 17px black;
}
.input{
    z-index: 2;
    text-align:center;
    position: relative;
    top: 50px;
}
.input input{
    font-family:sans-serif;
    width: 250px;
    font-size: 20px;
    padding: 5px;
    border: white;
    border-radius: 0px 15px 0px 15px;
    background: #fffefede;
    border: 2px solid #fffefede;
}
.input input:focus{
  background:#ffffffbd;
  color: black;
  border: 2px solid lightgray;
  outline: none;
}
.maindiv img{
  width: 350px;
  height:550px;
  z-index: 1;
  padding: 15px 15px;
  margin: auto;
  display: flex;
  align-items: center;
  position: relative;
  bottom:80px;
  border: 2px solid white;

}
*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  
}

body{
  font-family: 'montserrat', sans-serif;
}
@media only screen and (max-width: 500px){
  .deg{
    left:35%;
  }
  .main{
    background:linear-gradient(45deg, #7a868a, #8e7c87ad,#9e96ad,#8ba09e,#b7b7b3)
  }
}
@media only screen and (max-width: 800px) and (min-width: 500px){
  .deg{
    left:40%;
  }

}
</style>

<!-- js part -->
<script>
export default {
 data(){
  return{
      api_key: 'a3ecb4ef93ae2286d3393714794f9a05',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      weather:{},
      query:'Bangladesh,BD',
      dates:'',
      pic:"warm.b6e9602c",

  }
 },
mounted(){
     fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(data=>{
     return data.json()}).then(data=>{
       this.weather = data
  })
 },
 methods:{
  get(){
    fetch (`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(data=>{
      return data.json().then(data=>{
        this.weather = data
         if (this.weather.main.temp >= 30) {
      this.pic = "warm.b6e9602c"
    }
    else if (this.weather.main.temp <=30 && this.weather.main.temp >= 15) {
      this.pic = "clouds.445b4326"
    }
    else if (this.weather.main.temp <=15) {
      this.pic ="cold.ca1c41e7" 
    }
      })
    })
  },
  date(){
    this.dates = Date()
    return this.dates.slice(0,15)
  }
 }
}

</script>