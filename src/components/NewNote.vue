<template>
  <base-card>
  <base-button @click="setSelectedTab('stored-note')" :mode="storedButtonMode">Stored NOTE</base-button>
    <base-button @click="setSelectedTab('add-note')" :mode="addButtonMode">Add </base-button>
  </base-card>
  <keep-alive>
      <component :title="the" :is="selectedTab"></component>
  </keep-alive>
</template>
<script>
import StoredNote from './StoredNote';
import AddNote from './AddNote';


export default {
  components: {
    StoredNote,
    AddNote
  },
  data() {
    return {
      selectedTab: 'stored-note',
      initialValue:{id: '',
                    title: '',
                    description: '',
                    link: '',},
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.org',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
      initialValue:this.initialValue,
      'editResource':this.editResource,
      'updateResource':this.updateResource
    };
  },
  computed: {
    storedButtonMode() {
      
      return this.selectedTab === 'stored-note' ? null : 'flat';
    },
    addButtonMode() {
        console.log("run   ")
      return this.selectedTab === 'add-note' ? null : 'flat';
    },
  },
  watch: {
    selectedTab(value){
      if( value === 'stored-note')
      {
        this.initialValue.id = ''
        this.initialValue.title = ''
        this.initialValue.description = ''
        this.initialValue.link =''
      }
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title: title,
        description: description,
        link: url,
      };
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-note';
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex, 1);
    },
    updateResource(resId,title, description, url) {
      const resIndex = this.storedResources.findIndex(res => res.id === resId);

      this.storedResources[resIndex].title=title
      this.storedResources[resIndex].description=description
      this.storedResources[resIndex].link=url

      this.initialValue.id = ''
      this.initialValue.title = ''
      this.initialValue.description = ''
      this.initialValue.link =''

      this.selectedTab = 'stored-note';
    },
    editResource(resId) {
        const resIndex = this.storedResources.findIndex(res => res.id === resId);
        this.initialValue.id = this.storedResources[resIndex].id
        this.initialValue.title = this.storedResources[resIndex].title
        this.initialValue.description = this.storedResources[resIndex].description
        this.initialValue.link = this.storedResources[resIndex].link
      
        this.selectedTab = 'add-note';
    },
  },

};
</script>