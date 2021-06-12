<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        characters into each input field
      </p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okay</base-button>
    </template>
  </base-dialog>
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
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import AddResource from '@/components/learning-resources/AddResource.vue';
import StoredResources from '@/components/learning-resources/StoredResources.vue';
import BaseDialog from '@/components/ui/BaseDialog.vue';
export default {
  components: {
    StoredResources,
    AddResource,
    BaseDialog
  },
  data() {
    return {
      inputIsInvalid: false,
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
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource
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
    },
    addResource(title, description, link) {
      if (
        title.trim() === '' ||
        description.trim() === '' ||
        link.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }
      const resourceInfo = {
        id: new Date().toISOString(),
        title,
        description,
        link
      };
      this.storedResources.unshift(resourceInfo);
      this.selectedTab = 'stored-resources';
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
    removeResource(id) {
      const resIndex = this.storedResources.findIndex(res => res.id === id);
      this.storedResources.splice(resIndex, 1);
    }
  }
};
</script>

<style scoped></style>
