<template>
  <div class="wrapper">
    <header>
      <div class="inner-wrapper">
      <nav class="header__hamburger">
        <svg viewBox="0 0 12 10" class="hamburger__icon">
        <path d="M12,2 L1,2" class="upper" style="fill: none;stroke: #FFFFFF;stroke-linecap: round;"/>
        <path d="M12,5 L1,5" class="middle" style="fill: none;stroke: #FFFFFF;stroke-linecap: round;"/>
        <path d="M12,8 L1,8" class="lower" style="fill: none;stroke: #FFFFFF;stroke-linecap: round;"/>   
        </svg>
        </nav>
      <a href="#"><img class="header__logo" alt="Tea Society logo" src="../assets/logo.png"></a>
      <nav class="header__menu">
        <ul ref="mobNav">
          <li><a href="#">home</a></li>
          <li><a href="#">menu</a></li> 
          <li><a href="#">about us</a></li>
          <li><a href="#">contact</a></li>
        </ul>
      </nav>
      </div>
    </header>
    <main>
      <div class="inner-wrapper">
        <div class="slogan">
          <p ref="aniText">It's a good day to start off <br/> with milk tea</p>
        </div>
      <div class="homeBtn">
        <button class="menu">the menu</button>
        <button class="contact">contact</button>
      </div>
        <img class="milktea" alt="Milktea" src="../assets/milktea.png">
      </div>
    </main>
      <footer>
        <div class="inner-wrapper">
          <p>#teasociety</p>
        </div>
      </footer>
  </div>
</template>

<script>
import { gsap }  from 'gsap';

export default {
  name: 'HomePage',
  props: {
    msg: String
  },
  mounted(){
    var navIcon = document.querySelector('.header__hamburger'); 
    var {mobNav} = this.$refs;
    var mobNavLinks = document.querySelectorAll('.header__menu ul li a'); 
    var hamburgerUpper = document.querySelector('.hamburger__icon > .upper');
    var hamburgerMiddle = document.querySelector('.hamburger__icon > .middle');
    var hamburgerLower = document.querySelector('.hamburger__icon > .lower');
    var {aniText} = this.$refs;
    var aniImage = document.querySelector('.milktea');

    var tlOnLoad = gsap.timeline({paused:false});  
    tlOnLoad.from(aniText, {duration: 0.5, autoAlpha:0, y:25, ease:'Power1.easeInOut'}, 0)
            .from(aniImage, {duration: 0.5, autoAlpha:0, y:25, ease:'Power1.easeInOut'}, 0.1)

    var tlnav = gsap.timeline ({paused:true});
    tlnav.to(mobNav, {duration: 0.2, autoAlpha: 1, height:430, ease:'Power1.easeInOut'}, "-=0.1") 
         .fromTo(mobNavLinks, {y:-20}, {duration: 0.28  , autoAlpha: 1, y:1, ease:'Power1.easeOut'}, 0)
         .to(hamburgerUpper, {duration: 0.3, attr: {d: "M8,2 L2,8"}, ease:'Power1.easeInOut'},0)
         .to(hamburgerMiddle, {duration: 0.3, attr: {d: "M8,8 L2,2"}, autoAlpha: 0, ease:'Power1.easeInOut'},0)
         .to(hamburgerLower, {duration: 0.3, attr: {d: "M8,8 L2,2"}, ease:'Power1.easeInOut'},0)


    navIcon.addEventListener('click', navAnimation);

    var menuState = 0;

    function navAnimation(){
      if (menuState == 0){
        tlnav.timeScale(1).play(0);
        menuState = 1;
        // console.log('play')
        } else if (menuState == 1){
          tlnav.timeScale(2).reverse();
          menuState = 0;
          // console.log('reverse')
        }
       }

    var screenWidth = window.innerWidth;   
    // click outside menu to close
    var menuOpen = 1;
    document.querySelector(".header__menu ul").addEventListener('click', function(){
      if (screenWidth <= 600 && menuOpen == 1 ){
        navAnimation();
      }   
    }); 
    }
  } 
</script>
<style>
@import 'HomePage.scss';
</style>
