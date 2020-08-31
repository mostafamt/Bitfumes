<template>
  <v-toolbar>
    <v-toolbar-title>Bitfumes</v-toolbar-title>
    <v-spacer></v-spacer>

    <app-notification v-if="loggedIn"></app-notification>
    <div class="hidden-sm-and-down">
      
      <router-link 
      v-for="item in items"
      :key="item.title"
      :to="item.to"
      v-if="item.show">
        <v-btn flat>{{item.title}}</v-btn>
      </router-link>

    </div>
  </v-toolbar>
</template>

<script>
import User from '../Helpers/User';
import AppNotification from './AppNotification.vue';
  export default {
    data(){
      return{
        items:[
          {title: 'Forum', to:'/forum', show: true},
          {title: 'Ask Question', to:'/ask', show: User.loggedIn()},
          {title: 'Category', to:'/category', show: User.admin()},
          {title: 'Login', to:'/login', show: !User.loggedIn()},
          {title: 'Logout', to:'/logout', show: User.loggedIn()},
        ]
      }
    },
    components: {
      AppNotification,
    },
    computed: {
      show_hide(item){
        if( item.title === 'Category' ){
          return User.admin();
        } else {
          return User.loggedIn();
        }
      },
      loggedIn(){
        return User.loggedIn();
      }
    },
    created(){
      EventBus.$on('logout', () => {
        User.logout();
      });
    }
      
  }
</script>

<style>

</style>

