<template>
  <top-header title="Note keping"></top-header>
  <new-note></new-note>
  <bottom-footer></bottom-footer>
</template>

<script>
import TopHeader from './components/layouts/TopHeader.vue';
import BottomFooter from './components/layouts/bottomFooter.vue';
import NewNote from './components/NewNote.vue';


export default {
  components: {
    TopHeader,
    NewNote,
    BottomFooter,

  }
};
</script>
<style >
* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
  position:relative; 
  min-height: 100%;
}

body {
  margin:0;
  padding:0;
  
}
</style>