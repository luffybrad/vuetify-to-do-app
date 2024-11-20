<template>
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
      

</template>

<script setup>
  import { ref } from 'vue'

  const drawer = ref(null)

</script>

<script>
  export default {
    data() {
      return { 
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