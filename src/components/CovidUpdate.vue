<template> 
<div id="box">
    <div id="covidcontainer">
        <!-- <h3 >Covid19 Tracker</h3> -->
        <div id="Recovered">
            Total Confirmed:
            <br><br>
            <span id="number">{{confirm}} </span>
        </div>
        <div id="deaths">
            Covid-19 Deaths:
            <br><br>
            <span id="number">{{deaths}}</span>
        </div>
        </div>
      <div id="covidcontainer2">
        <!-- <h3 >Covid19 Tracker</h3> -->
        <div id="Recovered">
            Total Recovered:
            <br><br>
            <span id="number">{{recover}} </span>
        </div>
        <div id="deaths">
             New Covid19 Cases:
            <br><br>
            <span id="number">{{newcases}}</span>
    </div>
      </div></div>
    
</template>

<script>
export default {
    data() {
        return {
            deaths: 0,
            confirm: 0,
            recover: 0,
            newcases: 0,
        }
    },
    methods: {
        async getDC() {
            try{
                const res=await fetch('https://api.covid19api.com/summary');
                const actualdata=await res.json();
                this.confirm = await actualdata.Global.TotalConfirmed
                this.deaths = await actualdata.Global.TotalDeaths
                this.recover = await actualdata.Global.TotalRecovered
                this.newcases = await actualdata.Global.NewConfirmed

                console.log(this.recover)
                console.log(this.confirm)
                console.log(this.deaths)
            }catch(error){
                console.log(error);
            }
        }
    },
    created() {
        setInterval(() => this.getDC(), 60000);
        this.getDC()
    }
}
</script>

<style scoped>

#covidcontainer{
    display: flex;
    flex-direction: row;
    flex-wrap:nowrap;
    justify-content: center;
    align-items: center;
    position:absolute;
    top:36%;
    margin-left:66%;
    
    height:20vh;
    width:27%;
    /* background-image: linear-gradient(to right, aqua, skyblue); */
    /* border-radius: 8px; */
  
    padding: 1em;
     box-shadow:0 3px 6px 0 rgba(200, 200, 200, 0.7) ;
}
#covidcontainer2{
    display: flex;
    flex-direction: row;
    flex-wrap:nowrap;
    justify-content: center;
    align-items: center;
    position:absolute;
    top:63%;
     height:20vh;
       width:27%;
    margin-left:66%;
    border-top: none;
 
    padding: 1em;
     box-shadow:0 3px 6px 0 rgba(200, 200, 200, 0.7) ;
     /* z-index:-20; */
}

#Recovered{
    position: relative;
    
    text-align: center;
    font-size: 1em;
    width:40%;
    height:fit-content;
    background-image: linear-gradient(to left,#206A5D,#007965);
    /* background-color: #00AF91; */
   color:white;
    padding: 1rem;
    border-radius: 8px;
    margin-right: 1rem;
}
#deaths{
    position: relative;
    height:fit-content;
    text-align: center;
    font-size: 1em;
    width:40%;
    background-image: linear-gradient(to left, red, darkred);
    color: white;
    border-radius: 8px;
    padding: 1rem;
    
}

</style>