
<template>
    <div class="cube rotate-0">
        <div class="dot-1 mid-mid"></div>
        <div class="dot-2 mid-mid"></div>
        <div class="dot-3 mid-mid"></div>
        <div class="dot-4 mid-mid"></div>
        <div class="dot-5 mid-mid"></div>
        <div class="dot-6 mid-mid"></div>
    </div>
</template>

<script>
    import $ from 'jquery'

    export default {
        name: 'LogoSVG',
        props: { },
        created() {
            let count = 1;
            let duration = 1000;
            let timer;

            let startTimer = function(){
                timer = setInterval(()=>{
                    //console.log("created...."+ count);

                    // From 1 to 3
                    if (count == 1) {
                        $('.dot-2').removeClass('mid-mid');
                        $('.dot-2').addClass('left-bot');
                        $('.dot-3').removeClass('mid-mid');
                        $('.dot-3').addClass('right-top');
                        $('.dot-6').removeClass('mid-mid');
                        $('.dot-6').addClass('right-top'); //console.log(count);
                    }
                    // From 3 to 5
                    if (count == 2) {
                        $('.dot-4').removeClass('mid-mid');
                        $('.dot-4').addClass('left-top');
                        $('.dot-5').removeClass('mid-mid');
                        $('.dot-5').addClass('right-bot'); //console.log(count);
                    }
                    // From 5 to 4
                    if (count == 3) {
                        $('.dot-1').removeClass('mid-mid');
                        $('.dot-1').addClass('left-bot');

                        $('.cube').removeClass('rotate-180');
                        $('.cube').addClass('rotate-90'); //console.log(count);
                    }
                    // From 4 to 6
                    if (count == 4) {
                        $('.dot-1').removeClass('left-bot');
                        $('.dot-1').addClass('left-mid');
                        $('.dot-6').removeClass('right-top');
                        $('.dot-6').addClass('right-mid');

                        $('.cube').removeClass('rotate-90');
                        $('.cube').addClass('rotate-180'); //console.log(count);
                    }
                    // From 6 to 5
                    if (count == 5) {
                        $('.dot-1').removeClass('left-mid');
                        $('.dot-1').addClass('mid-mid');
                        $('.dot-6').removeClass('right-mid');
                        $('.dot-6').addClass('mid-mid'); //console.log(count);
                    }
                    // From 5 to 2
                    if (count == 6) {
                        $('.dot-4').removeClass('left-top');
                        $('.dot-4').addClass('left-bot');
                        $('.dot-5').removeClass('right-bot');
                        $('.dot-5').addClass('left-bot');
                        $('.dot-1').removeClass('mid-mid');
                        $('.dot-1').addClass('right-top');
                        $('.dot-6').removeClass('mid-mid');
                        $('.dot-6').addClass('right-top');

                        $('.cube').removeClass('rotate-180');
                        $('.cube').addClass('rotate-0'); //console.log(count);
                    }
                    // From 2 to 4
                    if (count == 7) {
                        $('.dot-4').removeClass('left-bot');
                        $('.dot-4').addClass('right-bot');
                        $('.dot-1').removeClass('right-top');
                        $('.dot-1').addClass('left-top'); //console.log(count);
                    }
                    // From 4 to 1
                    if (count == 8) {
                        $('.dot-1').removeClass('left-top');
                        $('.dot-1').addClass('mid-mid');
                        $('.dot-2').removeClass('left-bot');
                        $('.dot-2').addClass('mid-mid');
                        $('.dot-3').removeClass('right-top');
                        $('.dot-3').addClass('mid-mid');
                        $('.dot-4').removeClass('right-bot');
                        $('.dot-4').addClass('mid-mid');
                        $('.dot-5').removeClass('left-bot');
                        $('.dot-5').addClass('mid-mid');
                        $('.dot-6').removeClass('right-top');
                        $('.dot-6').addClass('mid-mid');

                        $('.cube').removeClass('rotate-0');
                        $('.cube').addClass('rotate-180'); //console.log(count);
                    }
                    
                    count++;
                    if (count == 9) count = 1;

                }, duration);
            }

            let stopTimer = function() { 
                clearInterval(timer);
                count = 1;
            }

            startTimer();

            setTimeout(()=>{
                $('.cube').on({
                    mouseenter: function(){
                        //console.log("hover in..");
                        stopTimer();

                        $('.cube').removeClass('rotate-180 rotate-90');
                        $('.cube').addClass('rotate-0');
                        $('.cube').removeClass('rotate-0');
                        $('.cube').addClass('rotate-in-out');

                        $('.dot-1').removeClass('left-top left-bot left-mid mid-mid right-top');
                        $('.dot-1').addClass('shake-left-top');

                        $('.dot-2').removeClass('left-bot mid-mid');
                        $('.dot-2').addClass('shake-right-top');

                        $('.dot-3').removeClass('right-top mid-mid');
                        $('.dot-3').addClass('shake-right-mid');

                        $('.dot-4').removeClass('left-top left-bot mid-mid right-top right-bot');
                        $('.dot-4').addClass('shake-right-bot');

                        $('.dot-5').removeClass('left-bot mid-mid right-bot');
                        $('.dot-5').addClass('shake-left-bot');

                        $('.dot-6').removeClass('right-top right-mid mid-mid');
                        $('.dot-6').addClass('shake-left-mid');
                    }
                    , 
                    mouseleave: function(){
                        //console.log("hover out..");

                        $('.cube').removeClass('rotate-in-out');
                        //$('.cube').addClass('rotate-0');

                        $('.dot-1').removeClass('shake-left-top');
                        $('.dot-1').addClass('mid-mid');
                        
                        $('.dot-2').removeClass('shake-right-top');
                        $('.dot-2').addClass('mid-mid');
                        
                        $('.dot-3').removeClass('shake-right-mid');
                        $('.dot-3').addClass('mid-mid');
                        
                        $('.dot-4').removeClass('shake-right-bot');    
                        $('.dot-4').addClass('mid-mid');
                        
                        $('.dot-5').removeClass('shake-left-bot');
                        $('.dot-5').addClass('mid-mid');
                        
                        $('.dot-6').removeClass('shake-left-mid');
                        $('.dot-6').addClass('mid-mid');

                        //$('.cube').removeClass('rotate-0');
                        $('.cube').addClass('rotate-180');
                        
                        startTimer();
                    }
                });
            }, 100);
            


            
        }
    }
    
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.cube {
    position: absolute;
    width:50px;
    height:50px;
    margin:0;
    padding:0;
    /* background-color: red; */
    transition: all 300ms ease-in-out;
}
.dot-1, .dot-2, .dot-3, .dot-4, .dot-5, .dot-6 {
    position: absolute;
    transition: all 300ms ease-in-out;
    background-color: white;
    border-radius: 50%;
    width: 10px;
    height: 10px;
    background: rgb(92,92,92);
    background: linear-gradient(145deg, rgba(92,92,92,1) 0%, rgba(205,217,246,1) 37%, rgba(244,246,255,1) 100%);
}
/** Positioning */
.left-top {   transform: translate(5px, 5px);  }
.left-mid {   transform: translate(5px, 20px); }
.left-bot {   transform: translate(5px, 35px); }
.right-top {  transform: translate(35px, 5px); }
.right-mid {  transform: translate(35px, 20px); }
.right-bot {  transform: translate(35px, 35px); }
.mid-mid {    transform: translate(20px, 20px); }
/** Rotate */
.rotate-0 {   transform: rotate(0deg); }
.rotate-90 {  transform: rotate(90deg); }
.rotate-180 { transform: rotate(180deg); }
/* .rotate {     animation: rotating 3s linear infinite;}
@keyframes rotating {
  from {
    -ms-transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  to {
    -ms-transform: rotate(360deg);
    -moz-transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
    -o-transform: rotate(360deg);
    transform: rotate(360deg);
  }
} */
.rotate-in-out {     animation: rotate 5s ease-in-out infinite;}
@keyframes rotate {
  0% {
    -ms-transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  60% {
    -ms-transform: rotate(360deg);
    -moz-transform: rotate(360deg);
    -webkit-transform: rotate(360deg);
    -o-transform: rotate(360deg);
    transform: rotate(360deg);
  }
  100% {
    -ms-transform: rotate(0deg);
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
  }
}

/** Moove animation */
.shake-left-top {
    transform: translate(11px, 4px); 
    animation: move-l-t 2s ease infinite alternate;
}
@keyframes move-l-t {
  0%   {transform: translate(11px, 4px);  }
  50%  {transform: translate(20px, 20px); }
  60%  {transform: translate(20px, 20px); }
  100% {transform: translate(11px, 4px);  }
}
.shake-left-mid {  
    transform: translate(0px, 20px);
    animation: move-l-m 2s ease infinite alternate;
    animation-delay: 1s;
}
@keyframes move-l-m {
  0%   {transform: translate(0px, 20px);  }
  50%  {transform: translate(20px, 20px); }
  60%  {transform: translate(20px, 20px); }
  100% {transform: translate(0px, 20px);  }
}
.shake-left-bot {  
    transform: translate(11px, 36px); 
    animation: move-l-b 2s ease infinite alternate;
}
@keyframes move-l-b {
  0%   {transform: translate(11px, 36px);  }
  50%  {transform: translate(20px, 20px); }
  60%  {transform: translate(20px, 20px); }
  100% {transform: translate(11px, 36px);  }
}
.shake-right-top { 
    transform: translate(31px, 4px);  
    animation: move-r-t 2s ease infinite alternate;
    animation-delay: 1s;
}
@keyframes move-r-t {
  0%   {transform: translate(31px, 4px);  }
  50%  {transform: translate(20px, 20px); }
  60%  {transform: translate(20px, 20px); }
  100% {transform: translate(31px, 4px);  }
}
.shake-right-mid { 
    transform: translate(38px, 20px); 
    animation: move-r-m 2s ease infinite alternate;
}
@keyframes move-r-m {
  0%   {transform: translate(38px, 20px);  }
  50%  {transform: translate(20px, 20px); }
  60%  {transform: translate(20px, 20px); }
  100% {transform: translate(38px, 20px);  }
}
.shake-right-bot { 
    transform: translate(30px, 37px); 
    animation: move-r-b 2s ease infinite alternate;
    animation-delay: 1s;
}
@keyframes move-r-b {
  0%   {transform: translate(30px, 37px);  }
  50%  {transform: translate(20px, 20px); }
  60%  {transform: translate(20px, 20px); }
  100% {transform: translate(30px, 37px);  }
}

</style>
