<template>
    <div>
        <div class="d-inline-block p-3 anim1" v-if="diceResult[0]">
            <div v-if="!isNaN(diceResult[0])">
                <span v-if="diceResult[1]!=null"> <b> 1. </b> </span> 
                <img v-if="diceResult[0] < 7" :src="dicePNGs[diceResult[0]]" alt="" /> 
                <img v-if="diceResult[0] > 6" :src="dicePNGs[0]" alt="" /> 
                <div v-if="diceResult[0] > 6" class="res res-num"> {{ diceResult[0] }} </div> 
            </div>
            <div v-if="isNaN(diceResult[0])">
                <span v-if="diceResult[1]!=null"> <b> 1. </b> </span> 
                <img :src="dicePNGs[0]" alt="" /> 
                <div class="res res-str"> {{ diceResult[0] }} </div> 
            </div>
        </div>

        <div class="d-inline-block p-3 anim2" v-if="diceResult[1]"> 
            <div v-if="!isNaN(diceResult[1])">
                <b> 2. </b> 
                <img v-if="diceResult[1] < 7" :src="dicePNGs[diceResult[1]]" alt="" /> 
                <img v-if="diceResult[1] > 6" :src="dicePNGs[0]" alt="" /> 
                <div v-if="diceResult[1] > 6" class="res res-num"> {{ diceResult[1] }} </div> 
            </div>
            <div v-if="isNaN(diceResult[1])">
                <b> 2. </b> 
                <img :src="dicePNGs[0]" alt="" /> 
                <div class="res res-str"> {{ diceResult[1] }} </div> 
            </div>
        </div>

        <div class="d-inline-block p-3 anim3" v-if="diceResult[2]"> 
            <div v-if="!isNaN(diceResult[2])">
                <b> 3. </b> 
                <img v-if="diceResult[2] < 7" :src="dicePNGs[diceResult[2]]" alt="" /> 
                <img v-if="diceResult[2] > 6" :src="dicePNGs[0]" alt="" /> 
                <div v-if="diceResult[2] > 6" class="res res-num"> {{ diceResult[2] }} </div> 
            </div>
            <div v-if="isNaN(diceResult[2])">
                <b> 3. </b> 
                <img :src="dicePNGs[0]" alt="" /> 
                <div class="res res-str"> {{ diceResult[2] }} </div> 
            </div>
        </div>

        <div class="d-inline-block p-3 anim4" v-if="diceResult[3]"> 
            <div v-if="!isNaN(diceResult[3])">
                <b> 4. </b> 
                <img v-if="diceResult[3] < 7" :src="dicePNGs[diceResult[3]]" alt="" />
                <img v-if="diceResult[3] > 6" :src="dicePNGs[0]" alt="" /> 
                <div v-if="diceResult[3] > 6" class="res res-num"> {{ diceResult[3] }} </div>  
            </div>
            <div v-if="isNaN(diceResult[3])">
                <b> 4. </b> 
                <img :src="dicePNGs[0]" alt="" /> 
                <div class="res res-str"> {{ diceResult[3] }} </div> 
            </div>
        </div>

        <div class="d-inline-block p-3 anim5" v-if="diceResult[4]"> 
            <div v-if="!isNaN(diceResult[4])">
                <b> 5. </b>
                <img v-if="diceResult[4] < 7" :src="dicePNGs[diceResult[4]]" alt=""/> 
                <img v-if="diceResult[4] > 6" :src="dicePNGs[0]" alt="" /> 
                <div v-if="diceResult[4] > 6" class="res res-num"> {{ diceResult[4] }} </div>
            </div>
            <div v-if="isNaN(diceResult[4])">
                <b> 5. </b>
                <img :src="dicePNGs[0]" alt="" /> 
                <div class="res res-str"> {{ diceResult[4] }} </div> 
            </div> 
        </div>

        <div class="d-inline-block p-3 anim6" v-if="diceResult[5]">
            <div v-if="!isNaN(diceResult[5])">
                <b> 6. </b> 
                <img v-if="diceResult[5] < 7" :src="dicePNGs[diceResult[5]]" alt="" />
                <img v-if="diceResult[5] > 6" :src="dicePNGs[0]" alt="" /> 
                <div v-if="diceResult[5] > 6" class="res res-num"> {{ diceResult[5] }} </div>  
            </div>
            <div v-if="isNaN(diceResult[5])">
                <b> 6. </b> 
                <img :src="dicePNGs[0]" alt="" /> 
                <div class="res res-str"> {{ diceResult[5] }} </div> 
            </div>
        </div>

    </div>
</template>


<script>

export default {
  name: 'Results3',
  props: { 
    diceResult: {
      type: Array,
      required: true
    },
    dicePNGs: {
      type: Array,
      required: true
    }
  }/* ,
  watch: {
    diceResult: function(newVal, oldVal) {
      console.log('value ' + oldVal + ' to ' + newVal);
    }
  } */
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.res{
  position: absolute;
  width: 50px;
  height: 50px;
  top: 26px;
  right: 26px;
  color: #fff;
  text-shadow: 	1px 0px 1px rgb(255, 69, 69), 
                0px 1px 1px rgb(255, 69, 69), 
                -1px 0px 1px rgb(255, 69, 69), 
                0px -1px 1px rgb(255, 69, 69);
}

.res-num {
  padding-top: 5px;
  font-size: 28px;
}

.res-str {
  padding-top: 12px;
  font-size: 100%;
}

.anim1,.anim2,.anim3,.anim4,.anim5,.anim6 { 
  position: relative; 
  opacity: 0;
  animation: opacity-easein 800ms ease-in forwards;
}
.anim1 { animation-delay: 1700ms; }
.anim2 { animation-delay: 1400ms; }
.anim3 { animation-delay: 1100ms; }
.anim4 { animation-delay:  800ms; }
.anim5 { animation-delay:  500ms; }
.anim6 { animation-delay:  200ms; }

@keyframes opacity-easein {
  0%  { opacity: 0; }
  50% { opacity: 0; }
  100%{ opacity: 1; }
}

img {
  border-radius: 6px;
  box-shadow: 0px 30px 30px 0px black;
}

@media only screen and (max-width: 420px) {

  .results div.d-inline-block {
    padding: 10px !important;
  }

  .res-num,
  .res-str {
    top: 20px !important;
    right: 20px !important;
  }

}

</style>
