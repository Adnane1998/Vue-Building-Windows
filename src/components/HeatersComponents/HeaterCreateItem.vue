<template>
<div>
  <b-button v-b-modal.modal-1>Add a new Heater</b-button>

  <b-modal id="modal-1" title="Create a new heater"   hide-footer>
   <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
   

      <b-form-group id="input-group-2" label="Heater Name:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.name"
          placeholder="Enter name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Room Id:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="form.roomId"
          :options="foods"
          required
        ></b-form-select>
      </b-form-group>

         <b-form-group id="input-group-4" label="HeaterStatus:" label-for="input-4">
        <b-form-select
          id="input-4"
             v-model="form.heaterStatus"
          :options="heaterStatus"
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
          roomId: null,
          heaterStatus:null,
          
        },
        foods: [ 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
         heaterStatus: [ 'ON', 'OFF'],
        show: true
      }
      
    },
      created: async function() {
    let response = await axios.get(`${API_HOST}/api/rooms`);
    let rooms = response.data;
    let rooms_id= []
    console.log(rooms.length)
    for(let i=0;i<rooms.length;i++)
    {

  rooms_id[i]= rooms[i]["id"]
    }

    this.foods=rooms_id
  },
    methods: {
      onSubmit(event) {
        event.preventDefault()
       console.log(this.form)
         axios.post(`${API_HOST}/api/heaters`,this.form, {
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
        this.form.food = null
    
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>

