<template>
  <div>
    <app-header title="RememberMe"></app-header>
    <stored-resources :resources="storedResources"></stored-resources>
  </div>
</template>

<script>
import StoredResources from '@/components/learning-resources/StoredResources.vue';
import AppHeader from '@/components/layouts/AppHeader.vue';

export default {
  components: {
    StoredResources,
    AppHeader
  },
  data() {
    return {
      storedResources: [
        {
          id: 'vue-documentation',
          title: 'Official Vue Guide',
          description: 'The official Vue.js documentation',
          link: 'https://v3.vuejs.org/'
        },
        {
          id: 'frontend-masters',
          title: 'Frontend Masters',
          description: 'Modern front-end engineering courses',
          link: 'https://frontendmasters.com/'
        }
      ]
    };
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>
