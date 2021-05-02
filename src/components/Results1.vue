<template>
    <div>
        <div class="d-inline-block p-3 anim1" v-if="diceResult[0]">
            <span v-if="diceResult[1]!=null"> <b> 1. </b> </span> 
            <img :src="dicePNGs[diceResult[0]]" alt="" /> 
        </div>
        <div class="d-inline-block p-3 anim2" v-if="diceResult[1]"> 
            <b> 2. </b> 
            <img :src="dicePNGs[diceResult[1]]" alt="" /> 
        </div>
        <div class="d-inline-block p-3 anim3" v-if="diceResult[2]"> 
            <b> 3. </b> 
            <img :src="dicePNGs[diceResult[2]]" alt="" /> 
        </div>
        <div class="d-inline-block p-3 anim4" v-if="diceResult[3]"> 
            <b> 4. </b> 
            <img :src="dicePNGs[diceResult[3]]" alt="" /> 
        </div>
        <div class="d-inline-block p-3 anim5" v-if="diceResult[4]"> 
            <b> 5. </b> 
            <img :src="dicePNGs[diceResult[4]]" alt="" /> 
        </div>
        <div class="d-inline-block p-3 anim6" v-if="diceResult[5]"> 
            <b> 6. </b> 
            <img :src="dicePNGs[diceResult[5]]" alt="" /> 
        </div>
    </div>
</template>


<script>

export default {
  name: 'Results1',
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

.anim1,.anim2,.anim3,.anim4,.anim5,.anim6 {  
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
  
}

</style>
