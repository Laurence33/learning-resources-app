<template>
  <base-card>
    <base-button :mode="getButtonMode('stored-resources')" @click="setSelectedTab('stored-resources')">Stored
      Resources</base-button>
    <base-button :mode="getButtonMode('add-resource')" @click="setSelectedTab('add-resource')">Add
      Resource</base-button>
  </base-card>
  <keep-alive>
    <component @add-resource="addResource" :is="selectedTab"></component>
  </keep-alive>
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
    },
    getButtonMode(tab) {
      return this.selectedTab === tab ? null : 'flat';

    },
    addResource(newResource) {
      const data = { id: Date.now(), ...newResource };
      console.log(data);
      this.storedResources.push(data);
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(res =>
        res.id == resId
      );
      if (resIndex >= 0) {
        this.storedResources.splice(resIndex, 1);
      }
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      removeResource: this.removeResource
    }
  }
}
</script>