<template>
    <div>
        <nav class="header">
            <div class="headerLogo">
                <router-link to="/">Trello</router-link>
            </div>
            <div class="headerAuth">
                <a href="" v-if="isAuth" @click.prevent="logout">Logout</a>
                <router-link v-else to="/login">Login</router-link>
            </div>
        </nav>
    </div>
</template>

<script>
import {mapState, mapGetters, mapMutations} from 'vuex'

export default {
    data() {
        return {
        }
    },
    computed : {
        ...mapGetters([
            'isAuth'
        ]),
        ...mapState({
            navbarColor : 'navbarColor',
            bodyColor : 'bodyColor'
        })
    },
    watch : {
        'bodyColor' : 'updateTheme'
    },
    mounted() {
        this.updateTheme()
    },
    methods : {
        ...mapMutations([
            'LOGOUT'
        ]),
        logout() {
            this.LOGOUT()
            this.$router.push('/login')
        },
        updateTheme() {
            this.$el.style.backgroundColor = this.navbarColor

            const body = document.querySelector('body')
            const container = document.querySelector('.container')
            if(body) body.style.backgroundColor = this.bodyColor
            if (container) container.style.backgroundColor = this.bodyColor
        }
    }
}
</script>

<style>
.header 
{
  flex: none;
  background-color: rgba(0,0,0,.15);
  height: 32px;
  padding: 4px;
}

.header a 
{
  display: block;
  height: 30px;
  line-height: 30px;
  text-decoration: none;
  color: rgba(255,255,255,.5);
}

.headerLogo
{
  position: absolute;
  left: 50%;
  top: 7px;
  margin-left: -30px;
  text-align: center;
  font-weight: bolder;
  font-size: 24px;
}

.headerLogo a:hover,
.headerLogo a:focus 
{
  color: rgba(255,255,255,.9);
}

.headerAuth
{
  position: absolute;
  right: 15px;
  top: 5px;
}

.headerAuth a 
{
  border-radius: 2px;
  padding: 0 10px;
  background-color: rgba(255,255,255, .5);
  color: white;
  transition: all .3s;
}

.headerAuth a:hover,
.headerAuth a:focus 
{
  background-color: rgba(255,255,255, .3);
}
</style>