<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resource')">Add Resource</base-button>
  </base-card>
  <component :is="selectedTab"></component>
</template>

<script>
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue';
export default {
  components: { AddResource, StoredResources },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official VueJs documentation.',
          link: 'https://vuejs.org/'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to Google...',
          link: 'https://www.google.com'
        }
      ]
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    }
  },

  provide() {
    return {
      resources: this.storedResources
    }
  }
}
</script>