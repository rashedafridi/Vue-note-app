<template>
    <note-resource
    v-for="note in resources"
      :key="note.id"
      :id="note.id"
      :title="note.title"
      :description="note.description"
      :link="note.link"
    ></note-resource>
</template>
<script>
import NoteResource from './NoteResource.vue';

export default {
  inject: ['resources'],
  components: {
    NoteResource
  }
}
</script>