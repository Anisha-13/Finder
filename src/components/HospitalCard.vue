<template>
    <div>
         <div class="container-fluid mt-5">
             <div id= "container" class="column text-center">
                 <div id="image-box">
                    <img id="hospital" :src="imgSrc" />
                </div>
                 <div id="content-box" >
                    <p class="elm" id="name" @click="renderDetails"><span style="color:rgba(0,0,0,0.5);"><strong> {{name}} </strong></span><span style="font-weight:900;  color:#F05454;"> ({{type}}) </span></p>
                    <p class="elm"> 
                        <span v-for="x in Number(ratings)" :key="x" > &#11088; </span>
                    </p>
                    <p class="elm" id="nbed"><span>🛏️ Beds: {{numBed}} </span></p>
                    <p class="elm" @click="renderMaps" id="loc"> &#128204;  {{city}}, {{location}}, <span style="font-weight:900; color:#F05454;">{{parseInt(pin)}}</span>  </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
   

    props: {
        id: Number,
        imgSrc: String,
        name: String,
        type: String,
        ratings: Number,
        numBed: Number,
        location: String,
        lat: String,
        long: String,
        city:String,
        pin: String,
    },

    data() {
        return {
            rateNum: Number(this.ratings),
        }
    },

    emits: ['render-details', 'render-map'],

    methods: {
        renderDetails() {
            this.$emit('render-details', this.id)
            
        },

        renderMaps() {
            this.$emit('render-map', this.lat, this.long)
        }
    }
}
</script>

<style scoped>
#heading{
   text-align: center;
}


#container{
 display:flex;
  flex-direction: row;
  margin-left:2%;
  width: 60%;
  box-sizing: border-box;
  background-color:white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin-bottom: 2em ;
  border-radius: 12px;
}

.elm {
   
   font-family:monospace;
   line-height: 1em;
    margin-bottom:1.2em;
    font-size: 5rem;
}

#name {
    font-size:1em;
    margin-bottom:1em;
    
}

#nbed {
    margin-top: 1em;
    font-size: 1em;
}

#name:hover {
    
    text-decoration: underline;
    cursor: pointer;
}

#loc:hover {
     text-decoration: underline;
    cursor: pointer;
}

#container:hover {
    box-shadow: 0 3px 10px rgba(0, 0, 0, 0.26);
}

#image-box{
    width:20%;
    height:25%;
    margin-right:0.5em;
}
#hospital{
    
    position: relative;
    margin-top: 0.9em;
    padding-left:0.7em;
    border-radius:10%;
    width:100%;
    height:7em;
}
#content-box{
   
    margin-top: 0.2em;
    margin-left:1em;
    text-align: left;
    word-break: keep-all;
    
    
}
#content-box p{
    font-size: 1em;
   word-break: keep-all;
    line-height:1em;
    font-weight: 500;
    /* position: relative; */
    word-wrap: break-word;
    
}



</style>
