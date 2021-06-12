<template>
  <div>
    <base-card>
      <base-button
        @click="setSelectedTab('stored-resources')"
        :mode="storedResourcesButtonMode"
        >Learning Resources</base-button
      >
      <base-button
        @click="setSelectedTab('add-resource')"
        :mode="addResourceButtonMode"
        >Add Resource</base-button
      >
    </base-card>
    <component :is="selectedTab"></component>
  </div>
</template>

<script>
import AddResource from '@/components/learning-resources/AddResource.vue';
import StoredResources from '@/components/learning-resources/StoredResources.vue';
export default {
  components: {
    StoredResources,
    AddResource
  },
  data() {
    return {
      selectedTab: 'stored-resources',
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
  },
  provide() {
    return {
      resources: this.storedResources
    };
  },
  computed: {
    storedResourcesButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResourceButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    }
  }
};
</script>

<style scoped></style>
