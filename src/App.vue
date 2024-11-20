<template>
  <v-app id="inspire">


    <v-navigation-drawer
    v-model="drawer"
    prepend
    app
    permanent
    >
    <template v-slot:prepend>
          <v-img
            src="@/assets/subs.jpeg"
          ></v-img>
        </template>
  <v-list-item 
  nav
  title="My To-Do" 
  subtitle="Enhance your productivity"
  >
 
</v-list-item>
  <v-divider></v-divider>
  <v-list
          density="compact"
          nav
        >
  <v-list-item prepend-icon="mdi-format-list-checks" to="/" title="To-Do"></v-list-item>
  <v-list-item prepend-icon="mdi-help-box" to="/about" title="About"></v-list-item>
  </v-list>
</v-navigation-drawer>


    <v-app-bar
        app
        color="teal-darken-4"
        density="comfortable"
        image
      >
        <template v-slot:image>
          <v-img
            src="@/assets/notes.png"
            gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
          ></v-img>
        </template>

        <template v-slot:prepend>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title
        >Tasks</v-app-bar-title>

        <v-spacer></v-spacer>


        <!--conditional searchfield  -->
          <SearchFIeld
          v-if="location.name === 'Todo'"
          v-model="taskTitle"
          @keyup="console.log(taskTitle)"
          />

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </v-app-bar>

    <v-main>
      <!--  routing -->
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script setup>
  import { ref } from 'vue'
  import SearchFIeld from "./components/SearchFIeld.vue";
  import { useRoute, useRouter } from 'vue-router';
  const drawer = ref(null)

  const taskTitle = ref("")


  const location = useRoute()

</script>



<script>
import Todo from './pages/Todo.vue';
import { components } from 'vuetify/dist/vuetify-labs.js';

  export default {
    data() {
      return { 
      drawer: true
      }

  }
  }
</script>