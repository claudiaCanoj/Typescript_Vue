<template>
    <div v-if="isLoggedIn">
      <a id="home" href="#">
        <router-link to="/products">Productos</router-link> |
        <router-link to="/profile">Profile</router-link>
        <a @click="logout">Logout</a>
      </a>
    </div>
    <div id="burger" :class="{
        'active': active
    }" @click="toggleActive">
        <button type="button" class="burger-button" title="Menu">
            <span class="burger-bar burger-bar--1">a</span>
            <span class="burger-bar burger-bar--2">b</span>
            <span class="burger-bar burger-bar--3">c</span>
        </button>
    </div>
</template>
<script>
    export default {
        name: 'NavBar',
        computed : {
            //isLoggedIn : function(){ return this.$store.getters.isAuthenticated}
            isLoggedIn : function(){ return true}
        },
        methods: {
            async logout (){
            //await this.$store.dispatch('LogOut')
            //this.$router.push('/login')
            }, 
            toggleActive () {
                this.$emit('toggle-menu')
            }
        }
    }
  </script>

  <style scoped>

    #burger{color: #444};


    .hidden {
        visibility: hidden;
    }

    button {
        cursor: pointer;
    }

    /* remove blue outline */
    button:focus {
        outline: 0;
    }

    .burger-button {
        position: relative;
        height: 30px;
        width: 40px;
        display: block;
        z-index: 99;
        border: 0;
        border-radius: 0;
        background-color: transparent;
        pointer-events: all;
        transition: transform .6s cubic-bezier(.165, .84, .44, 1);
    }

    .burger-bar {
        background-color: $burger-color;
        position: absolute;
        top: 50%;
        right: 6px;
        left: 6px;
        height: 3px;
        width: auto;
        margin-top: -1px;
        transition: transform .6s cubic-bezier(.165, .84, .44, 1), opacity .3s cubic-bezier(.165, .84, .44, 1), background-color .6s cubic-bezier(.165, .84, .44, 1);
    }

    .burger-bar--1 {
        -webkit-transform: translateY(-6px);
        transform: translateY(-6px);
        top: 40%;
    }

    .burger-bar--2 {
        transform-origin: 100% 50%;
        transform: scaleX(1);
    }

    .burger-button:hover .burger-bar--2 {
        transform: scaleX(1);
    }

    .no-touchevents .burger-bar--2:hover {
        transform: scaleX(1);
    }

    .burger-bar--3 {
        transform: translateY(6px);
        top: 60%;
    }

    #burger.active .burger-button {
        transform: rotate(-180deg);
    }

    #burger.active .burger-bar {
        background-color: lighten($primary, 10);
    }

    #burger.active .burger-bar--1 {
        transform: rotate(45deg);
        top: 50%;
    }

    #burger.active .burger-bar--2 {
        opacity: 0;
    }

    #burger.active .burger-bar--3 {
        transform: rotate(-45deg);
        top: 50%;
    }

    @media screen and (max-width: 991px) {
        #burger {
            display: block;
        }
    }

    @media screen and (min-width: 990px) {
        #burger {
            display: none;
        }
    }

  </style>
  