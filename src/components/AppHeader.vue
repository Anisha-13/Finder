<template>
<div id="header">
    <header>
        <div class="header">

            <img id="logo" src="https://img.icons8.com/pastel-glyph/2x/ffffff/stethoscope.png" alt="logo">
            <a href="#default" class="logo"><span class="Logo-text">Finder</span></a>
            <div class="header-right">
                <router-link class="active" to="/">Home</router-link>
                <router-link to="/government">Government Hospitals</router-link>
                <router-link to="/privatehos"> Private Hospitals</router-link>
            </div>
        </div>
        <div class="search">
            <div class="field1">
                <input type="text" name="search" id="search" placeholder="Hospital/Pharmacy" v-model="searchText">
            </div>
            <div class="field2">
                <button type="submit" class="find" @click="search">
                    <img class="img" src="https://img.icons8.com/android/2x/ffffff/search.png">
                </button>
            </div>
        </div>
    </header>
</div>
</template>

<script>
export default {

    data() {
        return {
             searchText: ""
        }
    },

    emits: ['trigger-search'],

    methods: {
        search() {
            this.$emit('trigger-search', this.searchText)
        }
    }
    
}
</script>


<style scoped>
/* Style the header with a grey background and some padding */
@import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&family=Philosopher&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap');

*{
    padding: 0;
    margin: 0;
   
}

.header {
    background-color:#343A40;
    /* padding: 5px 10px; */
    max-height: 3rem;
    display: flex;
    width:100%;
    
  }
  #header{
    position:sticky;
    top:0;
    margin:0px ;
    padding:0px;
    width: 100%;
    overflow-x: hidden;
    z-index: 10;
  }
  header{
    margin:0px;
    padding:0px;
    width:100%;
  }

  #logo{
    padding-top:0.3em ;
    height: 2em;
    width: 50px;
  }
  
  /* Style the header links */
  .header a {
    float: left;
    color: white;
    text-align: center;
    padding: 0.8em;
    text-decoration: none;
    font-family: 'Montserrat', sans-serif;
    font-size:0.7em;
    line-height: 1.7em;
   
  }
  .logo .Logo-text{
    font-family: 'Philosopher', sans-serif;
    font-weight:lighter;
    font-size: x-large;
    
    
  }
  .img{
    width: 1.8em;
  }
  .find{
    background-color: #343a4077;
    border: none;
    cursor: pointer;
    margin-right: 8vw;
    margin-left: 2%;
  }
  #search{
  background-color:#303335;
  color: white;
  padding: 3% 5% 3% 5%;
  overflow-x: visible;
  width:19em;
  border: none;
  outline: none;
  font-size: 0.8em;
  }

  #search:focus{
    border-bottom-style: solid;
    /* background-color: #363636; */
  }
  .search{
    position: relative;
    top: -2.0rem;
    float: right;
    display: flex;
    flex-direction: row;
   
    align-items: center;
  }
  

  /* Change the background color on mouse-over */
  .header a:hover {
    color:rgb(117, 245, 238);
    text-decoration-line: none;
 
  }
  
  
  
  /* Float the link section to the right */
  .header-right {
    float: right;
  }
  
  /* Add media queries for responsiveness - when the screen is 500px wide or less, stack the links on top of each other */
  @media screen and (max-width: 500px) {
    .header a {
      float: none;
      display: block;
      text-align: left;
    }
    .header-right {
      float: none;
    }
  }
</style>