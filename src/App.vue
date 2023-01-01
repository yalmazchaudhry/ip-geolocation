<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-icon x-large>mdi-search-web</v-icon>
        

        <h1>IP LookUp</h1>
      </div>

      <!-- <v-spacer></v-spacer> -->

     
    </v-app-bar>

    <v-main>
      <MainPage/>
    </v-main>
  </v-app>
</template>

<script>
import MainPage from './components/MainPage';

export default {
  name: 'App',

  components: {
    MainPage,
  },
 

 
};
</script>
