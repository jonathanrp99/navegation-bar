
<template>
<header>
  <nav class="nav-header">
    <ul v-show="!mobile" class="navigation">
      <li><router-link class="nav-link" :to="{ name: 'Home'}">Home</router-link></li>
      <li><router-link class="nav-link" :to="{ name: 'About'}">About</router-link></li>
      <li><router-link class="nav-link" :to="{ name: 'Porfolio'}">Porfolio</router-link></li>
      <li><router-link class="nav-link" :to="{ name: 'Contact'}">Contact</router-link></li>
    </ul>
    <div class="icon">
      <i @click="toggleMobileNav" 
      v-show="mobile"
      class="far fa-bars"
      :class="{'icon-active' : mobileNav }"></i>
    </div>
    <transition name="mobile-nav">
      <ul v-show="mobileNav" class="dropdown-nav">
        <div class="brand">
          <img src="../assets/logo.png" alt="" class="logo">
          <h2 class="brand-text">Welcome to this project </h2>
        </div>
        <i @click="closeMobileNav" class="far fa-times-circle close-icon"></i>
        <div class="nav-box">
          <li><router-link class="mobile-nav-link" :to="{ name: 'Home'}"
          @click="closeMobileNav" >Home</router-link></li>
          <li><router-link class="mobile-nav-link" :to="{ name: 'About'}" 
          @click="closeMobileNav" >About</router-link></li>
          <li><router-link class="mobile-nav-link" :to="{ name: 'Porfolio'}"  
          @click="closeMobileNav" >Porfolio</router-link></li>
          <li><router-link class="mobile-nav-link" :to="{ name: 'Contact'}" 
          @click="closeMobileNav" >Contact</router-link></li>
        </div>
      <div class="outsideOfNav" @click="closeMobileNav"></div>
     </ul>
    </transition>
  </nav>
</header>
</template>


<script>
import { ref, onMounted } from 'vue';

export default {
name: "Navigation",

setup() {
const mobile = ref(null)
const mobileNav = ref(null)
const windowWidth = ref(null)

onMounted (() => {
  window.addEventListener("resize", checkScreen);
  checkScreen();
  })
function toggleMobileNav() {
  mobileNav.value = !mobileNav.value
  }
function  closeMobileNav() {
  mobileNav.value = null;
  }
function checkScreen() {
  windowWidth.value = window.innerWidth;
  if (windowWidth.value < 750) {
  mobile.value = true;
  return;
  } 
    {
mobile.value = false;
mobileNav.value = false;
  }
}
return {
mobile,
mobileNav,
windowWidth,
toggleMobileNav,
closeMobileNav,
checkScreen
    }
  }
}
</script>


<style scoped>
@import url(../css/variable.css);

header {
  top: 0;
  left: 0;
  background-color: var(--eerie-black-dark);
  z-index: 100;
  width: 100%;
  position: fixed;
  height: 10vh;
  transition: .5s ease all;
  color: var(--gainsboro);
  display: flex;
}

.nav-header {
  position :relative;
  display: flex;
  flex-direction: row;
  padding: 12px 0;
  width: 90%;
  margin: 0 auto;
}

.navigation {
  display: flex;
  transition: 0.5s ease-in;
  flex: 1;
  justify-content:  flex-end;
}

ul,
.nav-link {
  font-weight: 500;
  color: var(--gainsboro);
  list-style: none;
  text-decoration: none;
}

li {
  padding: 16px;
  margin-left: 1rem;
}


.nav-link {
  transition: .5s ease all;
  padding-bottom: 4px;
  border-bottom: 1px solid transparent;
  font-size: 1.25rem;
}

.nav-link:hover {
  color: var(--brilliant-green);
  border-color: var(--brilliant-green);
  filter: drop-shadow(.75em .75em .7em)   
} 

.icon {
  display: flex;
  align-items: center;
  position: absolute;
  top: 0;
  left: 24px;
  height: 100%;
  color: var(--gainsboro);
}

.icon-active {
  color: var(--brilliant-green);
  filter: drop-shadow(.25em .25em .9em) 
}

i {
  cursor: pointer;
  font-size: 1.5rem;
  transition: 1s ease all;
}
i:hover{
  color: var(--brilliant-green);
  filter: drop-shadow(.25em .25em .9em)   
}


.dropdown-nav{
  display: flex;  
  justify-content: center;
  flex-direction: column;
  position: fixed;
  width: 100vw;
  height: 100vh;
  top: 0;
  left: 0;
}
.brand {
  display: flex;
  border-bottom: 1px solid var(--gainsboro);
  width: 100vw;
  height: 10vh;
  background-color: var(--eerie-black-dark);
  position: absolute;
  top: 0;
  left: 0;
}

.brand img {
  margin-left: 1rem;
  margin-top: .5rem;
  margin-right: 1rem;
  margin-bottom: .5rem;
}

.brand-text {
  display: flex;
  flex-direction: column;
  margin: 2px;
  font-size: 1rem;
  justify-content: center;
}

.dropdown-nav .close-icon {
  position: absolute;
  color: var(--eerie-black-dark);
  right: 10vw;
  top: 10vh;
  z-index: 1;
}

.dropdown-nav .close-icon:hover {
  color: rgb(164, 61, 61);
}

.dropdown-nav li {
  display: flex;
  flex-direction: columns;
  justify-content: space-between;
  margin-bottom: 1rem;
  margin-top: 1rem;
  color: var(--gainsboro);
}


.nav-box {
  background-color: var(--eerie-black-dark);
  width: 80vw;
  height: 90vh;
  position: absolute;
  bottom: 0;
  left: 0;
}

a.mobile-nav-link{
  color: var(--gainsboro);
  font-size: 1.1rem;
  transition: .5s ease all;
  padding: 1rem, 1rem 4px 1rem;
  border-bottom: 1px solid transparent;
  text-decoration: none;  
}

a.mobile-nav-link:hover {
  color: var(--brilliant-green);
  border-color: var(--brilliant-green);
  filter: drop-shadow(.75em .75em .7em)   
}

.outsideOfNav {
  filter: blur(7.825rem);
  height: 90vh;
  width: 20vw;
  position: absolute;
  right: 0;
  bottom: 0;
  background-color: rgba(101, 113, 87, 0.8);
}

.mobile-nav-enter-active {
  transition: .5s ease all;
}

.mobile-nav-leave-active {
  transition: .25s ease all;
}

.mobile-nav-enter-from,
.mobile-nav-leave-to 
{
  transform: translateX(-450px);
}

.mobile-nav-enter-to {
  transform: translateX(0);
}
</style>
