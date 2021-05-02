<template>
  <div id="app">
    
    <!-- npm run serve -->
    <!-- vue-cli-service serve -->
    <!-- vue-cli-service --host 188.167.253.33 --> <!--Mobile-->

    <!--header - navbar -->
    <div class="row header-nav">
        <div class="col-1 text-center" style="min-width: 85px;">
            <img alt="Game logo" :src="require('./assets/images/dice-' + logoDice + '.png')" />
        </div>
        <div class="col">
            <h1>{{ lng.app_title }}</h1> 
        </div>
        <div class="col-1 m-0 p-0" style="background-color: yellow">
            <!-- <div class="pull-right mt-2" style="min-width: 30px"> -->
              <button v-if="language == 'EN'" class="lang" v-on:click="setLanguage('SK')"> SK </button>
              <button v-if="language == 'SK'" class="lang" v-on:click="setLanguage('EN')"> EN </button>
                <!-- <select class="lang pull-rihgt" v-model="language" v-on:change="setLanguage(language)"> 
                  <option>SK</option>
                  <option>EN</option>
                </select> -->
            <!-- </div> -->
        </div>
    </div>

    <!-- content -->
    <div class="row">
      <!-- left navigation -->
      <div class="col-1 left-nav text-left" style="min-width: 90px;">
          <span class="ml-10">{{ lng.number }}</span><br>
          <span class="ml-10">{{ lng.of_dice }}</span><br>
          <!-- <img :src="require('./assets/images/dice-' + diceInPlay + '.png')" alt="" /> -->

          <div id="setting1-btn">
              <a href="#" v-on:click="toggleSetting1()"> 
                <!-- <img v-if="!setting1Show" :src="require('./assets/images/setting2a.png')" alt=""> -->
                <!-- <img v-if=" setting1Show" :src="require('./assets/images/setting2b.png')" alt=""> -->
                <img v-if="!setting1Show" :src="require('./assets/images/dice-'  + diceInPlay + '.png')" alt="" />
                <img v-if=" setting1Show" :src="require('./assets/images/dice2-' + diceInPlay + '.png')" alt="" />
              </a>
          </div>
      </div>
      <!-- body -->
      <div class="col bg-grayblue"> 
        <!-- settings -->
        <div class="row">
            <!-- setting 1 -->
            <div class="setting1 sett1-off" id="setting1">
                <div v-for="index in 6" :key="index" class="d-inline-block p-2 sett1-img">
                  <a href="#" v-on:click="diceInPlay = index"> 
                    <img :src="require('./assets/images/dice-' + index + '.png')" alt="" /> 
                  </a>
                </div>
            </div>

            <div class="col-12" v-if="width < 435"></div> 
            <!-- setting 2 -->
            <div class="setting2 sett2-off text-left" id="setting2" v-show="setting1Show==true">
                <a href="#" v-on:click="toggleSetting2()"> 
                    <img v-if="!setting2Show" :src="require('./assets/images/setting3a.png')" alt="" /> 
                    <img v-if=" setting2Show" :src="require('./assets/images/setting3b.png')" alt="" /> 
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
                  </div>
                </form>
            </div>
        </div>
        <!-- body 3 -->
        <div class="row">
          <div class="col-12 mt-4 text-center">
            <!-- button -->
            <button v-if="!gameStarted" class="btn btn-primary btn-lg w-25" v-on:click="roll()"> {{ lng.play }} </button>
            <button v-if=" gameStarted" class="btn btn-dark btn-lg w-25"> {{ lng.rolling }}.. </button>

            <!-- rolling dice -->
            <div class="dice mt-5" v-if="!diceRollEnd">
                <img class="dice1" :src="require('./assets/images/dice-' + diceSide1 + '.png')" alt="" /> 
                <img class="dice2" :src="require('./assets/images/dice-' + diceSide2 + '.png')" alt="" />
            </div>
            <!-- rolling dice END - NO Custom setting -->
            <div class="dice mt-5" v-if="!customSet && diceRollEnd">
                <img class="dice1" :src="require('./assets/images/dice-blank.png')" alt="" /> 
                <div class="result res-num"> {{ diceSum }} </div> 
            </div>
            <!-- rolling dice END - Custom setting - Numbers -->
            <div class="dice mt-5" v-if="customSet && diceRollEnd && !customStr">
                <img class="dice1" :src="require('./assets/images/dice-blank.png')" alt="" /> 
                <div class="result res-num"> {{ diceSum }} </div> 
            </div>
            <!-- rolling dice END - Custom setting - String -->
            <div class="dice mt-5" v-if="customSet && diceRollEnd && customStr">
                <img class="dice1" :src="require('./assets/images/dice-blank.png')" alt="" /> 
                <div class="result res-str" v-if="diceInPlay == 1 && resultHasString"> {{ diceResult[0] }} </div> 
                <div class="result res-num" v-if="diceInPlay  > 1 && resultHasString"> ? </div> 
                <div class="result res-num" v-if="!resultHasString"> {{ diceSum }} </div> 
            </div>

            <!-- DICES results -->
            <div class="col-12 mt-4 results">
                <!-- DICES NO Custom setting -->
                <Results1 :diceResult="diceResult" v-if="!customSet" />
                <!-- DICES Custom setting - Numbers -->
                <Results2 :diceResult="diceResult" v-if="customSet && !customStr" />
                <!-- DICES Custom setting - String -->
                <Results3 :dice="diceResult" v-if="customSet && customStr" />
            </div>

          </div>

        </div>

      </div>
      <!-- END body -->
    </div>
    <!-- END content -->
  </div>
</template>