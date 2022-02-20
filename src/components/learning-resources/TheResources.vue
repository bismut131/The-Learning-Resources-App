<template>
  <base-card>
    <base-button @click='setSelectedTab("stored-resources")' :mode='storedResButtonMode'>Stored Resources</base-button>
    <base-button @click='setSelectedTab("add-resource")' :mode='addResButtonMode'>Add Resource</base-button>
  </base-card>
  <keep-alive>
    <component :is='selectedTab'></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources';
import AddResource from './AddResource';

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
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google',
          link: 'https://google.com'
        }
      ]
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resources' ? null : 'flat';
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeResource
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, link) {
      this.storedResources.push({
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: link
      });
      this.setSelectedTab('stored-resources');
    },
    removeResource(resId) {
      const indexResource = this.storedResources.findIndex(res => resId === res.id);
      this.storedResources.splice(indexResource, 1);
    }
  }
};
</script>

<style scoped>

</style>