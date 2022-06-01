<template>
   <header>
   <nav class="nav-header">
     <div class="brand">
       <img src="../assets/logo.png" alt="" class="logo">
     </div>
     <ul v-show="!mobile" class="navigation">
        <li><router-link class="nav-link" :to="{ name: 'Home'}">Home</router-link></li>
        <li><router-link class="nav-link" :to="{ name: 'About'}">About</router-link></li>
        <li><router-link class="nav-link" :to="{ name: ''}">Porfolio</router-link></li>
        <li><router-link class="nav-link" :to="{ name: ''}">Contact</router-link></li>
     </ul>
     <div class="icon">
       <i @click="toggleMobileNav" 
        v-show="mobile"
        class="far fa-bars"
        :class="{'icon-active' : mobileNav }"
        >
        </i>
     </div>
     <transition name="mobile-nav">
     <ul v-show="mobileNav" class="dropdown-nav">
        <li><router-link class="nav-link" :to="{ Path: 'Home'}">Home</router-link></li>
        <li><router-link class="nav-link" :to="{ name: 'About'}">About</router-link></li>
        <li><router-link class="nav-link" :to="{ name: ''}">Porfolio</router-link></li>
        <li><router-link class="nav-link" :to="{ name: ''}">Contact</router-link></li>
      </ul>
     </transition>
   </nav>
   </header>
   <router-view />
</template>


<script>
import { ref } from 'vue';

export default {
  name: "Navigation",
           created() {
             window.addEventListener("resize", this.checkScreen);
             this.checkScreen();
           },

           mounted() {
             window.addEventListener('scroll', this.updateScroll)
           },
         methods: {
           toggleMobileNav() {
           this.mobileNav = !this.mobileNav;
          },

          updateScroll() {
            const scrollPosition = window.scrollY;
            if (scrollPosition > 50 ) {
              this.scrolledNav = true
              return;
            }
            this.scrolledNav = false;
            return;
          },

           checkScreen() {
           this.windowWidth = window.innerWidth;
           if (this.windowWidth < 750) {
             this.mobile = true;
             return;
           }
            this.mobile = false;
            this.mobileNav = false;
            return;
         },
      
        },
        setup() {
        const mobile = ref(null)
        const mobileNav = ref(null)
        const windowWidth = ref(null)

      return {
           mobile,
           mobileNav,
           windowWidth,
           
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
  transition: .5s ease all;
  color: var(--gainsboro);
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
      margin-left: 16px;
  }

  
  .nav-link {
      font-size: 14px;
      transition: .5s ease all;
      padding-bottom: 4px;
      border-bottom: 1px solid transparent;
      font-size: 20px;
  }

  .nav-link:hover {
          color: var(--brilliant-green);
          border-color: var(--brilliant-green);
          filter: drop-shadow(.75em .75em .7em)   
      } 


.nav-header {
  position :relative;
   display: flex;
  flex-direction: row;
  padding: 12px 0;
  width: 90%;
  margin: 0 auto;


}

.brand {
  display: flex;
  align-items: center;
}

.navigation {
  display: flex;
  transition: 0.5s ease-in;
  flex: 1;
  justify-content:  flex-end;
}

img {
  width: 50px;
  transition: 0.5s ease all;
}

.icon {
  display: flex;
  align-items: center;
  position: absolute;
  top: 0;
  right: 24px;
  height: 100%;
  color: var(--gainsboro);
}

i {
  cursor: pointer;
  font-size: 24px;
  transition: 1s ease all;
  z-index: 100;
}
i:hover{
   color: var(--brilliant-green);
    filter: drop-shadow(.25em .25em .9em)   
}

.icon-active {
  color: var(--brilliant-green);
    filter: drop-shadow(.25em .25em .9em) 
}

.dropdown-nav{

  display: flex;
  justify-content: center;
  flex-direction: column;
  position: fixed;
  max-width: 250px;
  height: 100%;
  background-color: var(--eerie-black-dark);
  top: 0;
  right: 0;
}

.dropdown-nav li {
  margin-left: 0;
  color: var(--gainsboro);
}

.mobile-nav-enter-active,
.mobile-nav-leave-active{
  transition: 1s ease all;
}

.mobile-nav-enter-from,
.mobile-nav-leave-to 
 {
  transform: translateX(750px);
}

.mobile-nav-enter-to {
  transform: translateX(0);
}
</style>
