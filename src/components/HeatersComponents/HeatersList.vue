<template>
  <div class="windows-list pt-3">
  
    
       <input type="text"

         placeholder="Filter by Room or Heater"
         v-model="filter" />

  
  <hr>
    <heaters-list-item
      v-for="heater in filteredRows"
      :heater="heater"
      :key="heater.id"  
      @heater-updated="updateHeater"
    >
    </heaters-list-item>
         <heater-create-item>
        </heater-create-item>

  </div>
</template>


<script>
import axios from 'axios';
import {API_HOST} from '../../config';
import HeatersListItem from './HeatersListItem';
import HeaterCreateItem from './HeaterCreateItem';


export default {
  components: {
   HeaterCreateItem,
      

    HeatersListItem
  },
  name: 'HeatersList',
  data: function() {
    return {
      /* Initialize windows with an empty array, while waiting for actual data to be retrieved from the API */
      heaters: [],
       filter:''
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/heaters`);
    let heaters = response.data;
    this.heaters = heaters;
  },
    computed: {
  filteredRows() {
    return this.heaters.filter(row => {
       const names= row.name.toString().toLowerCase();
         const room_names= row.roomName.toString().toLowerCase();
      
   
      const searchTerm = this.filter.toLowerCase();

      return room_names.includes(searchTerm) ||
        names.includes(searchTerm);
    });
  }
},
  methods: {
    updateHeater(newHeater) {
      /* Find the place of window objectw ith the same Id in the array, and replace it */
      let index = this.heaters.findIndex(heater => heater.id === newHeater.id);
      this.heaters.splice(index, 1, newHeater);
    }
  }
}
</script>
