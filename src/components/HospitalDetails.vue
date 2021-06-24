<template>
    
<div>

  <AppHeader @trigger-search="notAllowed"/>

  <div  class="Top-part"   
   > 
    <h1>Hospitals Are About Healing</h1>
    <h6>-IRWIN RENDLER</h6>
  </div>
  <div class="Container">
    <div class="Main-part">
      <div class="feild">
        <h2>{{name}}</h2>
      </div>
      <div class="feild" id="text">Ratings : 
        <span v-for="x in rating" :key="x">  &#11088; </span>
      </div>
      <div class="feild" id="text">Type : <span id="type"> {{type}}</span></div>
      <div class="feild">
        <h3><i>Location : {{city}}, {{state}}, {{parseInt(pincode)}}</i></h3>
      </div>
      <div class="feild feild1">
          <a :href="link" target="blank" @click="debug"> &#128279; click to visit hospital's webpage...</a>
      </div>
        <div class="feild">
          <p id="loc" @click="navigateLoc">  &#128279;  Click here to see location in map </p>
      </div>
    </div>
    <div class="Details-part">
      <span id="details">
        <h4>&#10024; DETAILS</h4>
      </span>
      <ul type=square>
        <li>Number of Beds : {{nBed}}</li>
        <li>Number of Doctors : {{nDoc}}</li>
      </ul>
      <span id="disease">
        <h4>🌡️ Diseases</h4>
      </span>
      <ul type=Square>
        <li v-for="(obj, index) in disease" :key="index">
          {{obj.disease}} : <span class="cost">{{obj.price}}</span>
        </li>
      </ul>
      <span id="treatment">
        <h4> 💉 Treatment</h4>
      </span>
      <ul type=square>
        <li v-for="(el, index) in treatment" :key="index">
          {{el}}
        </li>
      </ul>
    </div>
  </div>

</div>
</template>

<script>
import AppHeader from './AppHeader.vue'

export default {

  components: {
    AppHeader
  },

    data() {
      return {
        name: "",
        rating: 0,
        type: "",
        city: "",
        state: "",
        pincode: 0,
        nDoc: 0,
        nBed: 0,
        disease: [],
        treatment: [],
        link: "",
        image: "",
        l1: "http://www.google.com",
        nlat: "",
        nlong: "",
        lat: 0,
        long: 0,
      }
    },

    methods: {
      debug(event) {
        console.log(event.target.href)
      },

      notAllowed() {
        alert("This method not allowed here.")
    },
     navigateLoc() {
           console.log(this.nlat.split(" ")[0])
            let nlat1 = Number(this.nlat.split(" ")[0])
            let nlong1 = Number(this.nlong.split(" ")[0]) 
            console.log(this.nlong.split(" ")[0])
            this.getLocation()
            this.$router.push({name: 'Azuremaps', params:{
                plat: nlat1,
                plong: nlong1,
                lat: this.lat,
                long: this.long,
            }})
      },
      getLocation() {
            if (navigator.geolocation) {
                    navigator.geolocation.watchPosition(this.showPosition);
            } else { 
                console.log("Geolocation is not supported by this browser.")
             }
        },
        showPosition(position) {
            this.lat = position.coords.latitude 
            this.long = position.coords.longitude
        }
    },

    created() {
      this.name = this.$route.params.name
      this.rating = this.$route.params.rating
      this.type = this.$route.params.type
      this.city = this.$route.params.city
      this.state = this.$route.params.state
      this.pincode = this.$route.params.pincode
      this.nDoc = this.$route.params.nDoc
      this.nBed = this.$route.params.nBed
      this.disease = this.$route.params.disease
      this.treatment = this.$route.params.treatment
      this.link = "http://" + this.$route.params.link
      this.image = this.$route.params.image

      // make treatment to object
      this.treatment = this.treatment.replaceAll("[", "")
      this.treatment = this.treatment.replaceAll("]", "")
      this.treatment = this.treatment.replaceAll("'", "")
      this.treatment = this.treatment.replaceAll("\"", "")
      this.treatment = this.treatment.replaceAll(",", "")
      this.treatment = this.treatment.split("  ")

      // processing disease string
      this.disease = this.disease.replaceAll("[", "")
      this.disease = this.disease.replaceAll("]", "")
      this.disease = this.disease.replaceAll("'", "")
      this.disease = this.disease.replaceAll("\"", "")
      this.disease = this.disease.replaceAll(",", "")
      this.disease = this.disease.replaceAll(":", "")
      this.disease = this.disease.split("  ")
      var newArr = []
      for (var i = 0; i < this.disease.length; i+=2) {
        newArr.push({disease:this.disease[i], price:this.disease[i+1]})
      }
      this.disease = newArr

         this.nlat = this.$route.params.nlat
      this.nlong = this.$route.params.nlong
      this.getLocation()

      console.log(this.name)
      console.log(this.rating)
      console.log(this.type)
      console.log(this.city)
      console.log(this.state)
      console.log(this.pincode)
      console.log(this.nDoc)
      console.log(this.nBed)
      console.log(this.treatment)
      console.log(this.disease)
     
      console.log(this.treatment)
      console.log(this.link)
      console.log(this.$route.params.image)
      console.log(this.nlat)
      console.log(this.nlong)
    }
}  
</script>

<style scoped>

@import url('https://fonts.googleapis.com/css?family=Raleway:300&display=swap');

* {
  margin: 0;
  padding: 0;
  font-family:monospace;
}

#type{
  color:#F05454;
  font-weight: 900;
}
a {
    font-size: 1rem;
    font-family: monospace;
    text-decoration: none;
     

}
#loc {
   font-size: 1rem;
    font-family: monospace;
    text-decoration: none;
    cursor: pointer;
}

h1, h6 {
    font-family: Georgia, 'Times New Roman', Times, serif;
    
    color:#171717;
}
h2{
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-size: 1.3em;
  color:#900C3F;
}

h4 {
  font-family: Georgia, 'Times New Roman', Times, serif;
    font-size: 1.3rem;
    margin-bottom: 0.3rem;
}

li{
  margin-left: 5%;
  padding-left: 1%;
  text-align: left;
  color: black;
}
.Top-part {
  margin-right: auto;
  margin-left: auto;
  position:relative;
  top:-2.2em;
  height: 40vh;
  width: 97.5vw;
  background-size: cover;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
   background-image:
  url('https://images.pexels.com/photos/532568/pexels-photo-532568.jpeg?auto=compress&cs=tinysrgb&dpr=2&w=500');
 
}

h1, h6 {
  font-family: 'Raleway', sans-serif;
  line-height: 2.5rem;
  
}
.Container{
  display: flex;
  flex-direction:row;
 
}
.Main-part{
  width:50%;
  margin-top: 0%;
  margin-left:2%;
  background-color:rgba(238, 238, 238,0.5);
  overflow-wrap: break-word;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  /* border-radius: 8px; */
  /* background-image: linear-gradient(to left, dodgerblue, blueviolet); */
  color: black;
}
.feild{
  font-family: Georgia, 'Times New Roman', Times, serif;
  padding-top: 2%;
  padding-left:2%;
  font-size: 100%;
  text-align: left;
  
 
}
.feild1{
  padding-top: 4em;
  word-break: keep-all;
 
 
}
#text{
  font-size: 1.2em;
}
.Details-part{
  padding-top:1%;
  padding-left: 1%;
  margin-left: 2%;
  width: 50%;
  margin-top: 0%;
  margin-right: 2%;
  background-color:#F8EDED;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  /* border-radius: 8px; */
  /* background-image: linear-gradient(to right, blueviolet, dodgerblue); */
}
#details, #treatment, #disease {
  color:red;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  text-align: left;
}
</style>
