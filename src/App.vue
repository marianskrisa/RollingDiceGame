<template>
	<div id="app">
		
		<!-- npm run serve -->
		<!-- vue-cli-service serve -->
		<!-- vue-cli-service --host 188.167.253.33 --> <!--Mobile-->

		<!-- header - navbar -->
		<div class="header-nav text-left">
			<div class="logo text-left">
				<LogoSVG /> <!-- LOGO Animation -->
			</div>
			<div class="title text-left">
				<h1 v-if=" width >= 480"> {{ lng.app_title }} </h1> 
				<h2 v-if="(width <  480 && width >= 420) && language == 'EN' "> {{ lng.app_title }} </h2> 
				<h2 v-if="(width <  480 && width >= 400) && language == 'SK' "> {{ lng.app_title }} </h2> 
				<h4 v-if=" language == 'EN' && width <  420"> {{ lng.rolling_dice }} <br> {{lng.game}} </h4> 
				<h4 v-if=" language == 'SK' && width <  400"> {{ lng.rolling_dice }} <br> {{lng.game}} </h4> 
				
			</div>
			<div class="lang text-left">
				<button v-if="language == 'EN'" v-on:click="setLanguage('SK')"> SK </button>
				<button v-if="language == 'SK'" v-on:click="setLanguage('EN')"> EN </button>
				<br>
				<a href="#" v-on:click="setVolume()"> 
					<svg v-if="audioOn" id="svg-volume-up" xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#000000">
						<path d="M0 0h24v24H0z" fill="none"/>
						<path d="M3 9v6h4l5 5V4L7 9H3zm13.5 3c0-1.77-1.02-3.29-2.5-4.03v8.05c1.48-.73 2.5-2.25 2.5-4.02zM14 3.23v2.06c2.89.86 5 3.54 5 6.71s-2.11 5.85-5 6.71v2.06c4.01-.91 7-4.49 7-8.77s-2.99-7.86-7-8.77z"/>
					</svg>
					<svg v-if="!audioOn" id="svg-volume-down" xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#000000">
						<path d="M0 0h24v24H0z" fill="none"/>
						<path d="M16.5 12c0-1.77-1.02-3.29-2.5-4.03v2.21l2.45 2.45c.03-.2.05-.41.05-.63zm2.5 0c0 .94-.2 1.82-.54 2.64l1.51 1.51C20.63 14.91 21 13.5 21 12c0-4.28-2.99-7.86-7-8.77v2.06c2.89.86 5 3.54 5 6.71zM4.27 3L3 4.27 7.73 9H3v6h4l5 5v-6.73l4.25 4.25c-.67.52-1.42.93-2.25 1.18v2.06c1.38-.31 2.63-.95 3.69-1.81L19.73 21 21 19.73l-9-9L4.27 3zM12 4L9.91 6.09 12 8.18V4z"/>
					</svg>
				</a>
			</div>
		</div>

		<!-- content -->
		<div>
			<!-- left navigation -->
			<div class="left-nav text-left">
				<div class="left-nav-button">
					<span class="lbl-nr">{{ lng.number }}</span><br>
					<span class="lbl-dice">{{ lng.of_dice }}</span><br>

					<div id="setting1-btn">
							<a href="#" v-on:click="toggleSetting1()"> 
								<img v-if="!setting1Show" :src="require('./assets/images/PNG/Dice1-' + diceInPlay + '.png')" alt="" />
								<img v-if=" setting1Show" :src="require('./assets/images/PNG/Dice2-' + diceInPlay + '.png')" alt="" />
							</a>
					</div>
				</div>
					
				<!-- setting 1 -->
				<div id="setting1" class="sett1-off">
					<!-- repeat dices -->
					<div v-for="(Dice, index) in dice.PNGs" :key="index" class="d-inline-block sett1-img">
						<a href="#" v-on:click="toggleDicePNG(index)" v-show="index > 0"> 
							<!-- <img :src="require('./assets/images/dice-' + index + '.png')" alt="" />  -->
							<img :src="Dice" alt="" /> 
						</a>
					</div>
				</div>
				
				<!-- setting 2 -->
				<div id="setting2" class="sett2-show text-left" v-show="setting1Show==true">
					
					<a href="#" v-on:click="toggleSetting2()"> 
						<svg v-if="!setting2Show" id="svg-setting" xmlns="http://www.w3.org/2000/svg" enable-background="new 0 0 24 24" height="24px" viewBox="0 0 24 24" width="24px">
							<g>
								<path d="M0,0h24v24H0V0z" fill="none"/>
								<path d="M19.14,12.94c0.04-0.3,0.06-0.61,0.06-0.94c0-0.32-0.02-0.64-0.07-0.94l2.03-1.58c0.18-0.14,0.23-0.41,0.12-0.61 l-1.92-3.32c-0.12-0.22-0.37-0.29-0.59-0.22l-2.39,0.96c-0.5-0.38-1.03-0.7-1.62-0.94L14.4,2.81c-0.04-0.24-0.24-0.41-0.48-0.41 h-3.84c-0.24,0-0.43,0.17-0.47,0.41L9.25,5.35C8.66,5.59,8.12,5.92,7.63,6.29L5.24,5.33c-0.22-0.08-0.47,0-0.59,0.22L2.74,8.87 C2.62,9.08,2.66,9.34,2.86,9.48l2.03,1.58C4.84,11.36,4.8,11.69,4.8,12s0.02,0.64,0.07,0.94l-2.03,1.58 c-0.18,0.14-0.23,0.41-0.12,0.61l1.92,3.32c0.12,0.22,0.37,0.29,0.59,0.22l2.39-0.96c0.5,0.38,1.03,0.7,1.62,0.94l0.36,2.54 c0.05,0.24,0.24,0.41,0.48,0.41h3.84c0.24,0,0.44-0.17,0.47-0.41l0.36-2.54c0.59-0.24,1.13-0.56,1.62-0.94l2.39,0.96 c0.22,0.08,0.47,0,0.59-0.22l1.92-3.32c0.12-0.22,0.07-0.47-0.12-0.61L19.14,12.94z M12,15.6c-1.98,0-3.6-1.62-3.6-3.6 s1.62-3.6,3.6-3.6s3.6,1.62,3.6,3.6S13.98,15.6,12,15.6z"/>
							</g>
						</svg>
						<svg v-if="setting2Show" id="svg-close" xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 0 24 24" width="24px" fill="#000000">
							<path d="M0 0h24v24H0z" fill="none"/>
							<path d="M14.59 8L12 10.59 9.41 8 8 9.41 10.59 12 8 14.59 9.41 16 12 13.41 14.59 16 16 14.59 13.41 12 16 9.41 14.59 8zM12 2C6.47 2 2 6.47 2 12s4.47 10 10 10 10-4.47 10-10S17.53 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8z"/>
						</svg>
						<!-- <img v-if="!setting2Show" :src="require('./assets/images/setting3a.png')" alt="" /> 
						<img v-if=" setting2Show" :src="require('./assets/images/setting3b.png')" alt="" />  -->
					</a> 
					<span class="font-12" v-if="setting2Show"> {{ lng.customNames }}: </span> <br>
					
					<form class="mt-2" v-if="setting2Show">
						<div class="form-group">
							<div class="d-inline-block ml-2">
								<label for="name1"> 1. </label>
								<input type="text" maxlength="6" id="name1" v-model="diceNames[0]" />  
							</div>
							<div class="d-inline-block ml-2">
								<label for="name2"> 2. </label>
								<input type="text" maxlength="6" id="name2" v-model="diceNames[1]" />  
							</div>
							<div class="d-inline-block ml-2">
								<label for="name3"> 3. </label>
								<input type="text" maxlength="6" id="name3" v-model="diceNames[2]" />  
							</div>
							<div class="d-inline-block ml-2">
								<label for="name4"> 4. </label>
								<input type="text" maxlength="6" id="name4" v-model="diceNames[3]" />  
							</div>
							<div class="d-inline-block ml-2">
								<label for="name5"> 5. </label>
								<input type="text" maxlength="6" id="name5" v-model="diceNames[4]" />  
							</div>
							<div class="d-inline-block ml-2">
								<label for="name6"> 6. </label>
								<input type="text" maxlength="6" id="name6" v-model="diceNames[5]" />  
							</div>
							<div class="d-inline-block ml-2">
								<button class="btn btn-sm btn-dark" type="submit" v-on:click="resetInput()"> {{ lng.reset }} </button>
							</div>
						</div>
					</form>
				</div>

				<svg class="ln-svg" width="80" height="156" viewBox="0 0 80 156" fill="none" xmlns="http://www.w3.org/2000/svg">
					<path class="grey-blue" d="M63.9999 103.5C80.4999 40.5 3.99995 97 17.4999 48.5C30.9999 1.1006e-06 73.9999 100.5 79.9989 -3.35031e-07L79.9989 156.001L-13.0001 156.001C-13.0001 156.001 9.99994 150 17.4999 124.5C25 99.0001 47.4999 166.5 63.9999 103.5Z" />
					<path class="light-blue" d="M72.4999 105.5C84.4999 34.9999 20.9851 94.5 26 52.5C31.0149 10.5 74.1762 76.6191 79 52.5C80 47.5 80 35.5 80 35.5C80 76.1243 80 156.5 80 156.5L-21 156.5C-21 156.5 34 177 26 137.5C18 98 60.4999 176 72.4999 105.5Z" />
					<path class="grey-blue" d="M27.6112 91.4437C28.0933 86.8638 32.3328 83.6356 36.876 84.389L48.6666 86.3442C53.6064 87.1633 56.5881 92.2678 54.8752 96.973L51.5817 106.02C49.857 110.758 44.2332 112.738 39.9205 110.127L30.8439 104.63C28.1925 103.025 26.7071 100.032 27.0316 96.9497L27.6112 91.4437Z" />
					<path class="light-blue" d="M33.0319 92.1321C33.5628 87.672 37.6607 84.523 42.1072 85.1582L48.7457 86.1065C53.774 86.8248 56.8685 91.9865 55.1327 96.7601L51.7862 105.963C50.077 110.663 44.5225 112.66 40.2117 110.125L36.0057 107.65C33.2682 106.04 31.7425 102.963 32.1179 99.8092L33.0319 92.1321Z" />
					<circle class="grey-blue" cx="43" cy="97" r="2" />
					<circle class="grey-blue" cx="49.9999" cy="93" r="2" />
					<circle class="grey-blue" cx="37" cy="101" r="2" />
					<circle class="grey-blue" cx="40" cy="55" r="2" />
					<circle class="grey-blue" cx="46.9999" cy="51" r="2" />
					<circle class="grey-blue" cx="34" cy="59" r="2" />
					<circle class="grey-blue" cx="35" cy="47" r="2" />
					<circle class="grey-blue" cx="44" cy="61" r="2" />
					<circle class="grey-blue" cx="32" cy="135" r="2" />
					<circle class="light-blue" cx="73" cy="51" r="2" />
				</svg>
					
			</div>
			<!-- body 2 -->
			<div class="content"> 
					<div class="col-12 pt-5 text-center">
						
						<!-- button -->
						<button v-if="!gameStarted" class="btn btn-primary btn-lg w-25" v-on:click="roll()"> {{ lng.play }} </button>
						<button v-if=" gameStarted" class="btn btn-dark btn-lg w-25"> {{ lng.rolling }}.. </button>
						
						<!-- rolling dice -->
						<div class="dice mt-5" v-if="!diceRollEnd">
								<img class="dice1" :src="dice.PNGs_red100[diceSide1]" alt="" /> 
								<img class="dice2" :src="dice.PNGs_red100[diceSide2]" alt="" />
						</div>
						<!-- rolling dice END - NO Custom setting -->
						<div class="dice mt-5" v-if="!customSet && diceRollEnd">
								<img class="dice1" :src="dice.PNGs_red100[0]" alt="" /> 
								<div class="result res-num"> {{ diceSum }} </div> 
						</div>
						<!-- rolling dice END - Custom setting - Numbers -->
						<div class="dice mt-5" v-if="customSet && diceRollEnd && !customStr">
								<img class="dice1" :src="dice.PNGs_red100[0]" alt="" /> 
								<div class="result res-num"> {{ diceSum }} </div> 
						</div>
						<!-- rolling dice END - Custom setting - String -->
						<div class="dice mt-5" v-if="customSet && diceRollEnd && customStr">
								<img class="dice1" :src="dice.PNGs_red100[0]" alt="" /> 
								<div class="result res-str" v-if="diceInPlay == 1 && resultHasString"> {{ diceResult[0] }} </div> 
								<div class="result res-num" v-if="diceInPlay  > 1 && resultHasString"> ? </div> 
								<div class="result res-num" v-if="!resultHasString"> {{ diceSum }} </div> 
						</div>
						<div class="dice-shadow"></div>
						
						<!-- DICES results -->
						<div class="col-12 mt-4 results">
								<!-- DICES NO Custom setting -->
								<Results1 :diceResult="diceResult" :dicePNGs="dice.PNGs_white" v-if="!customSet" />
								<!-- DICES Custom setting - Numbers -->
								<Results2 :diceResult="diceResult" :dicePNGs="dice.PNGs_white" v-if="customSet && !customStr" />
								<!-- DICES Custom setting - String -->
								<Results3 :diceResult="diceResult" :dicePNGs="dice.PNGs_white" v-if="customSet && customStr" />
						</div>

					</div>

			</div>
			<!-- END body 2 -->
		</div>
		<!-- END body -->
	</div>
</template>



<script>
//============================================================================================== SCRIPT
//============================================================================================== SCRIPT
import Vue from 'vue'
import Results1 from './components/Results1.vue'
import Results2 from './components/Results2.vue'
import Results3 from './components/Results3.vue'
import LogoSVG from './components/LogoSVG.vue'
import lang from './json/locale.json'
import $ from 'jquery'

export default {
	name: 'App',
	components: {
		Results1,
		Results2,
		Results3,
		LogoSVG
	},
	data(){
		return{
			lng: lang.EN,
			language: 'EN',

			logoDice: 1,
			diceInPlay: 1,
			diceNames: ['1', '2', '3', '4', '5', '6'],
			diceResult: [null,null,null,null,null,null],
			diceSum: 0,

			diceSide1: 6,
			diceSide2: 3,
			diceRollEnd: false,
			gameStarted: false,

			setting1Show: false,
			setting2Show: false,

			customSet: false,
			customStr: false,
			resultHasString: false,

			width: 1300,

			dice: { 
				PNGs: ['','','','','','',''],
				PNGs_red: ['','','','','','',''],
				PNGs_white: ['','','','','','',''],
				PNGs_red100: ['','','','','','','']
			},

			audioOn: true,
			audioToPlay: null,
			audio: {
				sound1_one: require('./assets/audio/DiceRollSound_1_one.mp3'),
				sound1_all: require('./assets/audio/DiceRollSound_1_all.mp3'),
				sound2_one: require('./assets/audio/DiceRollSound_2_one.mp3'),
				sound2_all: require('./assets/audio/DiceRollSound_2_all.mp3')
			}
		}
	},
	methods: {
		// Set the language
		setLanguage(lan) {
			this.language = lan;
			this.lng = (lan == 'SK') ? lang.SK : lang.EN;
		},
		// Set sound
		setSound(nr) {
			if(nr == 11)	this.audioToPlay = this.audio.sound1_one;
			if(nr == 16)	this.audioToPlay = this.audio.sound1_all;
			if(nr == 21)	this.audioToPlay = this.audio.sound2_one;
			if(nr == 26)	this.audioToPlay = this.audio.sound2_all;
		},
		// Volume Up / Mute
		setVolume() {
			this.audioOn = !this.audioOn;
		},
		// Play sound
		playRollSound() {
			let audio = new Audio(this.audioToPlay);
				audio.play();
		},
		// Animate logo
		fillDicePNGs() {
			for (let i=0; i<7; i++) {
				this.dice.PNGs[i] = require('./assets/images/PNG/Dice1-' + i + '.png');
				this.dice.PNGs_red[i] = require('./assets/images/PNG/Dice1-' + i + '.png');
				this.dice.PNGs_white[i] = require('./assets/images/PNG/Dice2-' + i + '.png');
				this.dice.PNGs_red100[i] = require('./assets/images/PNG2/Dice1-' + i + '.png');
			}
		},
		// Toggle Png after click
		toggleDicePNG(index) {
			for (let i=1; i<7; i++) {
				if (i != index) {
					this.dice.PNGs[i] = this.dice.PNGs_red[i];
				} else {
					this.dice.PNGs[i] = this.dice.PNGs_white[i];
				}
			}
			setTimeout(()=>{
				this.diceInPlay = index;
			},10)
		},
		// Show / hide setting 1 menu
		toggleSetting1() { 
			$('#setting1').toggleClass('sett1-on sett1-off'); 
			if( $('#setting1').hasClass('sett1-on') ){
					this.setting1Show = true;
			}else{
					this.setting1Show = false;
					$('#setting2').removeClass('sett2-off');
					$('#setting2').removeClass('sett2-on');
					$('#setting2').addClass('sett2-show');
					$('#setting1').removeClass('sett1-plus35px');
					$('.left-nav-button').removeClass('left-nav-button-plus30px');
					this.setting2Show = false;
			}
		},
		// Show / hide setting 2 menu
		toggleSetting2() { 
			if( $('#setting2').hasClass('sett2-show') ){  
					$('#setting2').removeClass('sett2-show');
					$('#setting2').addClass('sett2-on');
					this.setting2Show = true;
					$('#setting1').addClass('sett1-plus35px');
					$('.left-nav-button').addClass('left-nav-button-plus30px');
			}else
			if( $('#setting2').hasClass('sett2-on') ){    
					$('#setting2').removeClass('sett2-on');
					$('#setting2').addClass('sett2-off');
					this.setting2Show = false;
					$('#setting1').removeClass('sett1-plus35px');
					$('.left-nav-button').removeClass('left-nav-button-plus30px');
			}else
			if( $('#setting2').hasClass('sett2-off') ){   
					$('#setting2').removeClass('sett2-off');
					$('#setting2').addClass('sett2-on');
					this.setting2Show = true;
					$('#setting1').addClass('sett1-plus35px');
					$('.left-nav-button').addClass('left-nav-button-plus30px');
			}
		},
		// Close settings
		closeSettings() { 
			if( $('#setting1').hasClass('sett1-on') ){
				$('#setting1').toggleClass('sett1-on sett1-off'); 
				this.setting1Show = false;
				$('#setting2').removeClass('sett2-off');
				$('#setting2').removeClass('sett2-on');
				$('#setting2').addClass('sett2-show');
				$('#setting1').removeClass('sett1-plus35px');
				$('.left-nav-button').removeClass('left-nav-button-plus30px');
				this.setting2Show = false;
			}
		},
		// Clear input
		resetInput() {
			this.diceNames = ['1', '2', '3', '4', '5', '6'];
		},
		// Roll the dices - start game
		roll() {
			let count = 0;
			this.diceSum = 0;
			this.diceResult = [null,null,null,null,null,null],
			this.diceRollEnd = false;
			this.gameStarted = true;
			this.customSet = false;
			this.customStr = false;

			// Close settings
			this.closeSettings();
				
			// Play audio
			if (this.audioOn) { 
				if (this.diceInPlay == 1) { 
					this.setSound(21);
					this.playRollSound();
				} else {
					this.setSound(26);
					this.playRollSound();
				}
			}
			
			// First check custom settings
			for (let i = 0; i < 6; i++) {
				this.customSet = (this.diceNames[i] != (i+1)+'') ? (this.customSet || true) : (this.customSet || false);   // check if value changed
				this.customStr = (isNaN( this.diceNames[i] )) ? (this.customStr || true) : (this.customStr || false); // check if value is not number
			}
			//console.log(this.customSet+"");
			//console.log(this.customStr+"");

			// Set interval for the dice to roll
			let diceRoll = setInterval(()=>{
				count++;
				$('.dice').addClass('dice-roll');

				if(count==1){  	$('.dice1').addClass('d-close');
								$('.dice2').addClass('d-open');
				}else
				if(count==3){ 	this.diceSide1 = 3; this.diceSide2 = 1; 
								$('.dice1').removeClass('d-close');
								$('.dice2').removeClass('d-open');
				}else
				if(count==4){  	$('.dice1').addClass('d-close');
								$('.dice2').addClass('d-open');
				}else
				if(count==6){  	this.diceSide1 = 1; this.diceSide2 = 5; 
								$('.dice1').removeClass('d-close');
								$('.dice2').removeClass('d-open');
				}else
				if(count==7){  	$('.dice1').addClass('d-close');
								$('.dice2').addClass('d-open');
				}else
				if(count==9){  	this.diceSide1 = 5; this.diceSide2 = 2;
								$('.dice1').removeClass('d-close');
								$('.dice2').removeClass('d-open');
				}else
				if(count==10){ 	$('.dice1').addClass('d-close');
								$('.dice2').addClass('d-open');
				}else
				if(count==12){ 	this.diceSide1 = 2; this.diceSide2 = 4;
								$('.dice1').removeClass('d-close');
								$('.dice2').removeClass('d-open');
				}else
				if(count==13){ 	$('.dice1').addClass('d-close');
								$('.dice2').addClass('d-open');
				}else
				if(count==15){ 	this.diceSide1 = 4; this.diceSide2 = 6;
								$('.dice1').removeClass('d-close');
								$('.dice2').removeClass('d-open');
				}else
				if(count==16){ 	$('.dice1').addClass('d-close');
								$('.dice2').addClass('d-open');
				}else
				if(count==18){ 	this.diceSide1 = 6; this.diceSide2 = 3;
								$('.dice1').removeClass('d-close');
								$('.dice2').removeClass('d-open');
								count = 0;
				}
			}, 100);

			// Get random numbers and calculate the sum
			setTimeout(()=>{
				// If not custom setting
				if (!this.customSet) {
					for (let i = 0; i < this.diceInPlay; i++) {
						Vue.set(this.diceResult, i, Math.floor(Math.random() * 6) + 1);
						this.diceSum += this.diceResult[i];
					}
				// If custom setting
				}else{
					// If only numbers
					if (!this.customStr) {
						for (let i = 0; i < this.diceInPlay; i++) {
							Vue.set(this.diceResult, i, parseFloat( this.diceNames[ Math.floor(Math.random() * 6) ] ));   
							this.diceSum += this.diceResult[i];
						}
					// If string
					}else{
						let isString = 0;
						for (let i = 0; i < this.diceInPlay; i++) {
							let random = this.diceNames[ Math.floor(Math.random() * 6) ] ;
							// Check whether input is string or number
							if (isNaN(random)){
								Vue.set(this.diceResult, i, random);
								isString++;
							}else{
								Vue.set(this.diceResult, i, parseFloat(random));
								this.diceSum += parseFloat(random);
							}
						}
						this.resultHasString = (isString > 0) ? true : false;
					}
				}
			}, 3000);

			// Set 5sec timeout for the gameplay and stop the interval after
			setTimeout(()=>{
				clearInterval(diceRoll);
				$('.dice').removeClass('dice-roll');
				$('.dice1').removeClass('d-close');
				$('.dice2').removeClass('d-open');
				this.diceSide1 = 6; 
				this.diceSide2 = 3;
				this.gameStarted = false;
				this.diceRollEnd = true;
			}, 4600);
		},

		myEventHandler() {
			this.width = window.innerWidth; //console.log(this.width);
		},
	},
	// Others ...
	beforeMount(){
		this.fillDicePNGs();
		this.toggleDicePNG(1);
		this.width = window.innerWidth; //console.log(this.width);
	},
	created() {
		window.addEventListener("resize", this.myEventHandler);
	},
	destroyed() {
		window.removeEventListener("resize", this.myEventHandler);
	}

}
</script>


<style>
/* ============================================================================================== STYLE CSS */
/* ============================================================================================== STYLE CSS */
:root {
	--navy-blue: rgb(66, 70, 123);
	--dark-blue: rgb(12, 15, 49);
	/* --dark-blue: rgb(7, 6, 46); */
	--light-blue: rgb(218, 217, 226);
	--light-info-blue: rgb(59, 148, 243);
	--grey-blue: rgb(180, 174, 211); 
	--blood-red: rgb(175, 15, 15); 
}

#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	margin-top: 0px;
	background-color: var(--light-blue) !important;
}
/** Header */
.header-nav {
	background-color: var(--dark-blue);
	color: var(--light-blue);
	min-height: 70px;
}
.header-nav .logo {
	width: 80px;
	height: 70px;
	padding-top: 10px;
	padding-left: 15px;
	float: left;
}
.header-nav .title {
	min-height: 70px;
	float: left;
}
.header-nav .title h1 { float: left; margin: 10px 0px 0px 0px; }
.header-nav .title h2 { float: left; margin: 15px 0px 0px 0px; }
.header-nav .title h4 { float: left; margin: 5px 0px 0px 0px; }

.header-nav .lang {
	position: absolute;
	right: 0px;
	width: 60px;
	height: 70px;
	padding-top: 10px;
}
.header-nav .lang button{
	background-color: transparent !important;
	color: var(--grey-blue) !important;
	border: none !important;
	outline: none !important;
}
.header-nav .lang button:focus {
	border: none !important;
	outline: none !important;
}
.header-nav .lang button:hover{
	color: var(--light-blue) !important;
}
.header-nav .lang #svg-volume-up{
	margin-left: 5px;
	fill: var(--grey-blue);
}
.header-nav .lang #svg-volume-up:hover{
	fill: var(--light-blue);
}
.header-nav .lang #svg-volume-down{
	margin-left: 5px;
	fill: var(--grey-blue);
}
.header-nav .lang #svg-volume-down:hover{
	fill: var(--light-blue);
}

/** Content */
.left-nav {
	position: absolute;
	left: 0;
	width: 80px;
	height: 100vh;
	padding-left: 5px;
	border-top: 2px solid var(--light-blue);
	background-color: var(--dark-blue);
	color: var(--light-blue);
	text-align: center;
	float: left;
	z-index: 10;
}
.left-nav-button {
	position: absolute;
	left: 0;
	width: 80px;
	padding-top: 10px;
	padding-left: 5px;
	background-color: var(--dark-blue);
	color: var(--light-blue);
	float: left;
	z-index: 10;
}
.left-nav-button .lbl-nr {
	margin-left: 10px;
	transition: 0.4s ease-in;
}
.left-nav-button .lbl-dice {
	margin-left: 10px;
	transition: 0.4s ease-in;
}
.left-nav a img {
	width: 50px;
	height: 50px;
	margin: 10px;
	opacity: 0.9;
	box-shadow: 1px 1px 5px 0px black;
}
.left-nav a img:hover {
	opacity: 1;
	box-shadow: 1px 1px 15px -5px red;
	transition: 300ms ease-in;
}
.left-nav .ln-svg {
	position: absolute;
	left: 0;
	bottom: 0;
}
.light-blue {
	fill: var(--light-blue);
}
.grey-blue {
	fill: var(--navy-blue);
}

.ml-10 {
	margin-left: 10px;
}

#setting1 {
	position: absolute;
	top: 0;
	left: 80px;
	height: 160px;
	padding-top: 3px;
	background-color: var(--dark-blue);
	color: var(--light-blue);
	float:left
}
.sett1-plus35px {
	height: 195px !important;
	border-top-right-radius: 0px !important;
	border-bottom-right-radius: 0px !important;
}
.sett1-on{
	transition: 0.4s ease-in;
	width: 110px;
	opacity: 1;
	border-bottom-right-radius: 20px;
	border-top-right-radius: 20px;
}
.sett1-on div a img {
	width: 30px;
	height: 30px;
	animation: opacity-easein 800ms ease-in forwards; 
	box-shadow: 1px 1px 5px 0px black;
}

@keyframes opacity-easein{
	0%  { opacity: 0; }
	50% { opacity: 0; }
	100%{ opacity: 0.9; }
}
.sett1-on div a img:hover {
	transform: rotate(5deg);
}
.sett1-off {
	transition: 0.4s ease-out;
	width: 0;
	opacity: 0;
}
.sett1-off div img {
	display: none;
}

#setting2 {
	position: absolute;
	top: 0;
	left: 190px;
	padding-top: 5px;
	background-color: var(--dark-blue);
	color: var(--grey-blue);
}
.sett2-show {
	transition: 0.4s ease-in;
	width: 40px;
	height: 40px;
	border-radius: 50%;
	opacity: 1 !important;
	animation: opacity-easein 800ms ease-in forwards; 
}
.sett2-on{
	transition: 0.4s ease-in;
	width: 200px;
	height: 195px;
	border-top-right-radius: 20px;
	border-bottom-right-radius: 20px;
}
.sett2-off {
	transition: 0.4s ease-out;
	width: 40px;
	height: 40px;
	border-radius: 50%;
}

#setting2 #svg-setting {
	margin-top: 2px;
	margin-left: 8px;
	fill: var(--light-blue);
}
#setting2 #svg-setting:hover {
	fill: var(--light-info-blue);
	transition: 300ms ease-in-out;
	transform: rotate(120deg);
}
#setting2 #svg-close {
	margin-top: 2px;
	margin-left: 8px;
	fill: var(--blood-red);
}
/* #setting2 #svg-close:hover {
	transition: 300ms ease-in-out;
	transform: rotate(90deg);
} */


.font-12{
	font-size: 12px;
}

#setting2 form, 
#setting2 span {
	transition: 0.4s ease-in;
	opacity: 0;
	animation: opacity-easein 800ms ease-in forwards; 
}

form input {
	max-width: 70px;
	background: var(--light-blue);
	border-radius: 5px;
	text-align: center;
}

form button {
	position: relative;
	max-width: 68px;
	width: 68px;
	margin-top: 2px;
	background: var(--light-blue);
	border-radius: 5px;
	text-align: center;
	left: 107px;
}

@media only screen and (max-width: 420px) {
	.left-nav-button {
		width: 150px;
		height: 80px;
		background-color: var(--dark-blue);
		border-top-right-radius: 20px;
		border-bottom-right-radius: 20px;
		transition: 0.4s ease-in;
	}
	.left-nav-button-plus30px {
		width: 190px !important;
		border-bottom-right-radius: 0px !important;
	}
	.left-nav-button .lbl-nr {
		position: absolute;
		top: 12px;
		left: 80px;
		margin-left: 0 !important;
		transition: 0.4s ease-in;
	}
	.left-nav-button .lbl-dice {
		position: absolute;
		top: 35px;
		left: 80px;
		margin-left: 0 !important;
		transition: 0.4s ease-in;
	}
	.left-nav-button div {
		position: absolute;
		top: 5px;
	}
	#setting1 {
		border-top: 1px solid var(--light-blue);
		top: 85px;
		left: 15px;
		height: 0px;
		padding-top: 13px;
		z-index: 15;
	}
	.sett1-on{
		width: 60px;
		height: 382px !important;
		border-bottom-right-radius: 0px !important;
		border-top-right-radius: 0px !important;
	}
	
	#setting2 {
		top: 67px;
		left: 60px;
		padding-top: 5px;
		z-index: 20;
	}
	.sett2-show {
		animation: opacity-easein 500ms ease-in forwards; 
		opacity: 1 !important;
	}
	.sett2-on{
		transition: 0.4s ease-in;
		width: 130px;
		height: 400px;
		border-top-right-radius: 0px !important;
	}

	form label {
		opacity: 0;
	}
	form input {
		max-width: 80px;
		margin-bottom: 20px;
		background-color: var(--light-blue);
		border-radius: 5px;
		text-align: center;
	}

	form button {
		position: relative;
		max-width: 78px;
		width: 78px;
		background: var(--light-blue);
		border-radius: 5px;
		text-align: center;
		left: 14px;
	}

}
.content {
	padding-top: 80px;
	padding-left: 80px;
	position: relative;
	background-color: var(--light-blue);
	height: 100vh;
}
.content button {
	min-width: 110px;
	box-shadow: 0px 2px 5px 0px black;
}

.dice {
	margin: auto;
	position: relative;
	width: 100px;
	height: 100px;
	border-radius: 10px;
	background-color: var(--blood-red);
	z-index: 1;

}

.dice-roll {
	animation: roll 1s linear infinite;
}
@keyframes roll {
	100% { transform: rotate(360deg);   }
}

.dice1 {
	position: absolute;
	top: 0;
	left: 0;
	height: 100px;
	width: 100px;
	border-radius: 10px;
}
.dice-shadow {
	width: 90px;
	height: 10px;
	margin: auto;
	position: relative;
	background-color: var(--light-blue);
	box-shadow: 0px 60px 50px 30px var(--dark-blue);
	z-index: 0;
	top: -50px;
}
.dice1.d-close {
	animation: dclose 100ms linear 1 forwards;
}
@keyframes dclose {
	0%   { width: 100px; }
	100% { width:   0px; }
}

.dice2{
	position: absolute;
	top: 0;
	right: 0;
	height: 100px;
	width: 0px;
}

.dice2.d-open {
	animation: dopen 100ms linear 1 forwards;
}
@keyframes dopen {
	0%   { width: 0px;   }
	100% { width: 100px; }
}

.result {
	margin: auto;
	position: relative;
	width: 100px;
	height: 100px;
	border-radius: 50%;
	text-align: center;
	color: #fff;
}

.results img {
	width: 50px;
	height: 50px;
	margin: 10px;
}

.res-num{
	padding-top: 6px;
	font-size: 60px;
}

.res-str{
	padding-top: 22px;
	font-size: 200%;
}


</style>
