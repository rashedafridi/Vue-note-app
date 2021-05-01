<template>
  <base-dialog
    v-if="inputIsInvalid"
    title="Invalid Input"
    @close="confirmError"
  >
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        characters into each input field.
      </p>
    </template>
    <template #footer>
      <base-button @click="confirmError">close 😥</base-button>
    </template>
  </base-dialog>
  <base-card>
     <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input id="title" name="title" type="text" ref="titleInput" :value="title" />
      </div>
      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" name="description" rows="3" ref="descInput" :value="description"></textarea>
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input id="link" name="link" type="url" ref="linkInput" :value="Url" />
      </div>
      <div>
        <base-button type="submit"> {{UpdateOrADD}} </base-button>
      </div>
    </form>
 </base-card>
  
</template>
<script>
export default {
 
  inject: ['addResource','updateResource','initialValue'],
  data() {
    return {
      inputIsInvalid: false,
    };
  },
  computed:{
      title(){
        if(this.initialValue.title.length > 0)
        {
          return this.initialValue.title
        }
        else {
          // return this.$refs.titleInput.value;
          return ''
        }
      },
      description(){
        if(this.initialValue.description.length > 0)
        {
          return this.initialValue.description
        }
        else {
          return ''
        }
      },
      Url(){

        if(this.initialValue.link.length > 0)
        {
          return this.initialValue.link 
        }
        else {
          // return this.$refs.linkInput.value;
          return '';
        }

      },
      UpdateOrADD(){

        if(this.initialValue.id.length > 0)
        {
          return 'update'
        }
        else {
          // return this.$refs.linkInput.value;
          return 'Add note';
        }

      }

  },
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.descInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        return;
      }

      if( this.initialValue.id.length > 0){
        this.updateResource(this.initialValue.id, enteredTitle, enteredDescription, enteredUrl);
      }else{
         this.addResource(enteredTitle, enteredDescription, enteredUrl);
      }
     
    },

    confirmError() {
      this.inputIsInvalid = false;
    }
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #bf5fff;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>  
