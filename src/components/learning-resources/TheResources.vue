<template>
  <base-card>
    <base-button @click="selectTab('stored-resources')" :mode="storedResState"
      >Stored Resources</base-button
    >
    <base-button @click="selectTab('add-resource')" :mode="addResState"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

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
          id: 'vuejs.org',
          title: 'VueJS Docs',
          description: 'Complete official documentation of a framework, so neat, look at it!',
          link: 'https://vuejs.org'
        },
        {
          id: 'google.com',
          title: 'cssreference.io',
          description: 'I am sure you know it, I am also convinced you have not mastered it :)',
          link: 'https://cssreference.io/'
        },
        {
          id: 'developer.mozilla.org',
          title: 'MDN',
          description: 'You may not be sure but I want you to believe me - you will need it...',
          link: 'https://developer.mozilla.org/ru/'
        }
      ]
    };
  },
  methods: {
    selectTab(tabTagName) {
      this.selectedTab = tabTagName;
    },
    addResource(title, descr, link) {
      const newResource = {
        id: new Date().toString,
        title: title,
        description: descr,
        link: link
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeRes(resId) {
      const index = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(index, 1);
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      removeResource: this.removeRes
    };
  },
  computed: {
    storedResState() {
      return this.selectedTab === 'stored-resources' ? '' : 'flat';
    },
    addResState() {
      return this.selectedTab === 'add-resource' ? '' : 'flat';
    }
  }
};
</script>
