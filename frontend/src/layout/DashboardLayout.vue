<template>
  <div class="wrapper" :class="{ 'nav-open': $sidebar.showSidebar }">
    <side-bar
      :background-color="sidebarBackground"
      short-title="Argon"
      title="Argon"
    >
      <template slot="links">
        <sidebar-item :link="{ name: 'Dashboard', icon: 'ni ni-tv-2 text-black', path: '/dashboard'}"/>
        <sidebar-item :link="{name: 'Dictionaries', icon: 'ni ni-book-bookmark text-purple', path: '/dictionaries'}"/>
        <!-- <sidebar-item :link="{name: 'User Profile', icon: 'ni ni-single-02 text-blue', path: '/profile'}"/> -->
        <sidebar-item :link="{name: 'Labels', icon: 'ni ni-tag text-orange', path: '/labels'}"/>
        <sidebar-item :link="{name: 'Chapters', icon: 'ni ni-bullet-list-67 text-gray', path: '/chapters'}"/>
        <sidebar-item :link="{name: 'Training', icon: 'ni ni-hat-3 text-brown', path: '/training'}"/>
        <sidebar-item :link="{name: 'Explore', icon: 'ni ni-world text-green', path: '/explore'}"/>
        <sidebar-item :link="{name: 'Login', icon: 'ni ni-key-25 text-blue', path: '/login'}"/>
        <sidebar-item :link="{name: 'Register', icon: 'ni ni-circle-08 text-red', path: '/register'}"/>
        <sidebar-item :link="{name: 'Register', icon: 'ni ni-diamond', path: '/icons'}"/>
        <sidebar-item :link="{name: 'Register', icon: 'ni ni-diamond', path: '/tables'}"/>
        <sidebar-item :link="{name: 'Register', icon: 'ni ni-diamond', path: '/maps'}"/>

      </template>
    </side-bar>
    <div class="main-content" :data="sidebarBackground">
      <dashboard-navbar></dashboard-navbar>

      <div @click="toggleSidebar">
        <fade-transition :duration="200" origin="center top" mode="out-in">
          <!-- your content here -->
          <router-view></router-view>
        </fade-transition>
        <content-footer v-if="!$route.meta.hideFooter"></content-footer>
      </div>
    </div>
  </div>
</template>
<script>
  import DashboardNavbar from './DashboardNavbar.vue';
  import ContentFooter from './ContentFooter.vue';
  import { FadeTransition } from 'vue2-transitions';

  export default {
    components: {
      DashboardNavbar,
      ContentFooter,
      FadeTransition
    },
    data() {
      return {
        sidebarBackground: 'vue' //vue|blue|orange|green|red|primary
      };
    },
    methods: {
      toggleSidebar() {
        if (this.$sidebar.showSidebar) {
          this.$sidebar.displaySidebar(false);
        }
      }
    }
  };
</script>
<style lang="scss">
</style>
