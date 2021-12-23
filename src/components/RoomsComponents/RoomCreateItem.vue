<template>
<div>
  <b-button v-b-modal.modal-1>Add a new Room</b-button>

  <b-modal id="modal-1" title="Create a new Room" hide-footer>
   <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
   

      <b-form-group id="input-group-2" label="Room Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>








      <b-form-group id="input-group-3" label="Floor:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.floor"
          :options="floor"
          required
        ></b-form-select>
      </b-form-group>

     
       <br>
      <b-button type="submit" variant="primary"  >Submit</b-button>
    
    </b-form>
 
  </div>
  </b-modal>
</div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../../config';
  export default {
    data() {
      return {
        form: {
     
          name: '',
          floor: [ ],
           
          
        },
        floor: [ 1, 2,3,4,5,6],
  
        show: true
      }
      
    },
      created: async function() {
    let response = await axios.get(`${API_HOST}/api/rooms`);
  
  },
    methods: {
      onSubmit(event) {
        event.preventDefault()
       console.log(this.form)
         axios.post(`${API_HOST}/api/rooms`,this.form, {
   headers: {
          // remove headers
        }
      })
                .then((res) => {
                       window.location.reload()



                 })
                 .catch((error) => {
                     // error.response.status Check status code
                 }).finally(() => {
                     //Perform action in always
                 });
     
   
      },
 
      onReset(event) {
        event.preventDefault()
        // Reset our form values
      
        this.form.name = ''
        this.form.floor = null
     
    
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>

