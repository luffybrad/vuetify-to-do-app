<template>
  <v-app id="inspire">


    <v-navigation-drawer
    v-model="drawer"
    app
    permanent
    >
  <v-list-item 
  prepend-avatar="https://randomuser.me/api/portraits/men/85.jpg"
  nav
  title="My To-Do" 
  subtitle="Enhance your productivity"
  ></v-list-item>
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
        density="prominent"
        image="https://cdn.pixabay.com/photo/2013/07/12/13/56/note-147603_1280.png"
      >
        <template v-slot:image>
          <v-img
            gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
          ></v-img>
        </template>

        <template v-slot:prepend>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>Tasks</v-app-bar-title>

        <v-spacer></v-spacer>


        <v-text-field
        v-if="isTextFieldVisible"
        v-model="searchText"
        append-inner-icon="mdi-close"
        @click:append-inner="toggleSearchField"
        placeholder="Search"
        clearable
      ></v-text-field>

      <v-btn
      v-else
      @click="toggleSearchField"
       icon>
        <v-icon
        style="cursor: pointer;"
      >
        mdi-magnify
      </v-icon>
      </v-btn>
      


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

  const drawer = ref(null)

</script>

<script>
  export default {
    data() {
      return { 
      drawer: true,
      searchText: '',
      isTextFieldVisible: false,
    }
  },
  methods: {
    toggleSearchField() {
      this.isTextFieldVisible = !this.isTextFieldVisible;
      if (!this.isTextFieldVisible) {
        this.searchText = ''; // Clear search text when hiding
      }
    },
  },
  }
</script>