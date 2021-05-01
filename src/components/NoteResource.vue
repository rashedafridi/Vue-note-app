<template>
    <base-card>
        <header>
            <h3>{{title}}</h3>
            <div>
            <base-button mode="flat" @click="deleteResource(id)">Delete</base-button>
            <base-button mode="flat" @click="editResource(id)">Update</base-button>
            </div>
            
        </header>
         <p>{{ description }}</p>
      <nav>
        <a target="_blank" :href="link">View </a>
      </nav>
    </base-card>
</template>
<script>
export default {
  props: ['id', 'title', 'description', 'link'],
  inject: ['deleteResource', 'editResource']
};
</script>
<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

h3 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
}

p {
  margin: 0.5rem 0;
}

a {
  text-decoration: none;
  color: #ce5c00;
}

a:hover,
a:active {
  color: #c89300;
}
</style>