<template>
  <div>
    <div> 
      <header class="main">
        <nav @click="inMenuView = !inMenuView" id="hamburger" role="navigation">
          <div id="menuToggle">
            <input type="checkbox" />
            <span></span>
            <span></span>
            <span></span>
            <ul id="menu">
              <br><br>
              <a href="#"><li>Home</li></a>
              <a href="#"><li>Tour</li></a>
              <a href="#"><li>Shop</li></a>
              <a href="#"><li>Videos</li></a>
              <a href="#"><li>Links</li></a>
              <a href="#"><li>News</li></a>
              <div :style="`position: fixed; bottom: ${ forestActive ? -5 : -22 }%; transition: 500ms;`">
                <img style="width: 100vw;" src="./assets/kosherforesttt.png" alt="danny">
              </div>
            </ul>
          </div>
        </nav>
        <img class="logo" :src="require(`./assets/kosherlogos/kosherlogo${ inMenuView ? 5 : 6 }.png`)" alt="kosher logo">
      </header>
      <div class="picture-container">
        <img class="daniyel-pictures" src="./assets/daniyel1.jpg" alt="daniyel">
        <img class="daniyel-pictures" src="./assets/daniyel2.png" alt="daniyel">
        <img class="daniyel-pictures" src="./assets/daniyel3.jpg" alt="daniyel">
      </div>

     </div>
  </div>
</template>

<script>

import soundFile from './assets/audio.mp3'
import { useSound } from '@vueuse/sound'

export default {
  name: 'App',
  setup() {

    const { play, stop } = useSound(soundFile, { interrupt: true, volume: 0.25 });

    return {
      play, 
      stop
    }
  },
  data() {
    return {
      inMenuView: false,
      forestActive: false,
    }
  },
  mounted() {
    
  },
  unmounted() {

  },
  watch: {
    inMenuView() {
      this.inMenuView ? this.play() : this.stop();
      if (this.inMenuView) {
        setTimeout(() => {
          if (this.inMenuView) this.forestActive = true;
        }, 500);
      } else {
        this.forestActive = false;
      }
    }
  }
}
</script>

<style>
@font-face {
  font-family: "DaniyelsCustomFont";
  src: url('./assets/kosherworld.otf');
}

body {
  margin: 0;
  padding: 0;
  background-color: #cdcdcd;
  font-family: 'DaniyelsCustomFont';
}

.logo {
  position: relative;
  transform: translateX(50%);
  top: -80%;
  width: 50%;
}

#hamburger {
  position: fixed;
  top: -3.5%;
  left: -6%;
}

.center {
  display: flex;
  justify-content: center;
  align-items: center;
  align-content: center;
}

.daniyel-pictures {
  width: 100vw;
}

.main {
  position: fixed;
  top: 0;
  background-color: rgb(0, 0, 0);
  height: 7%;
  width: 100vw;
}


#menuToggle
{
  display: block;
  position: relative;
  top: 50px;
  left: 50px;
  
  z-index: 1;
  
  -webkit-user-select: none;
  user-select: none;
}

#menuToggle a
{
  text-decoration: none;
  color: #cdcdcd;
  margin: 1%;
  transition: color 0.3s ease;
}

#menuToggle a:hover
{
  color: rgb(255, 118, 64);
}

#menuToggle input
{
  display: block;
  width: 40px;
  height: 32px;
  position: absolute;
  top: -7px;
  left: -5px;
  
  cursor: pointer;
  
  opacity: 0; /* hide this */
  z-index: 2; /* and place it over the hamburger */
  
  -webkit-touch-callout: none;
}

/*
 * Just a quick hamburger
 */
#menuToggle span
{
  display: block;
  width: 33px;
  height: 4px;
  margin-bottom: 5px;
  position: relative;
  
  background: #cdcdcd;
  border-radius: 3px;
  
  z-index: 1;
  
  transform-origin: 4px 0px;
  
  transition: transform 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
              background 0.5s cubic-bezier(0.77,0.2,0.05,1.0),
              opacity 0.55s ease;
}

#menuToggle span:first-child
{
  transform-origin: 0% 0%;
}

#menuToggle span:nth-last-child(2)
{
  transform-origin: 0% 100%;
}

/* 
 * Transform all the slices of hamburger
 * into a crossmark.
 */
#menuToggle input:checked ~ span
{
  opacity: 1;
  transform: rotate(45deg) translate(-2px, -1px);
  background: #cdcdcd;
}

/*
 * But let's hide the middle one.
 */
#menuToggle input:checked ~ span:nth-last-child(3)
{
  opacity: 0;
  transform: rotate(0deg) scale(0.2, 0.2);
}

/*
 * Ohyeah and the last one should go the other direction
 */
#menuToggle input:checked ~ span:nth-last-child(2)
{
  transform: rotate(-45deg) translate(0, -1px);
}

/*
 * Make this absolute positioned
 * at the top left of the screen
 */
#menu
{
  position: absolute;
  height: 100vh;
  width: 100vw;
  margin: -100px 0 0 -50px;
  padding: 50px;
  padding-top: 125px;
  
  background: #000000;
  list-style-type: none;
  -webkit-font-smoothing: antialiased;
  /* to stop flickering of text in safari */
  
  transform-origin: 0% 0%;
  transform: translate(-100%, 0);
  
  transition: transform 0.5s cubic-bezier(0.77,0.2,0.05,1.0);
}

#menu li
{
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px 0;
  font-size: 22px;
}

/*
 * And let's slide it in from the left
 */
#menuToggle input:checked ~ ul
{
  transform: none;
  position: fixed;
  left: 0%;
}
</style>
