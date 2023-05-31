<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButton"
    >
      Stored Resources</base-button
    ><base-button @click="setSelectedTab('add-resource')" :mode="addResButton">
      Add Resources</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script lang="js">
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
    components: {
        StoredResources,
        AddResource,
    },
    data() {
        return {
        selectedTab: 'stored-resources',
        storedResources: [
            {
            id: 'official-guide',
            title: 'Official-guide',
            description: 'The official documentation to Vue JS',
            link: 'https://vuejs.org',
            },
            {
            id: 'google',
            title: 'Google',
            description: 'Learn to google...',
            link: 'https://vuejs.org',
            },
        ],

        };
    },
    methods: {
        setSelectedTab(tab) {
          this.selectedTab = tab;
        },
        addResource(title,description,url){
            const newResource = {
                id: new Date().toISOString(),
                title,
                description,
                link: url,
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        },
        removeResource(resId){
              const resIndex = this.storedResources.findIndex(
                (res) => res.id === resId
              );
              this.storedResources.splice(resIndex, 1);
        },
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource: this.addResource,
            deleteResource: this.removeResource,
        };
    },
    computed: {
        storedResButton() {
            return this.selectedTab === 'stored-resources' ? null : 'flat'
        },
        addResButton() {
            return this.selectedTab === 'add-resource' ? null : 'flat'
        }
    },
};
</script>
