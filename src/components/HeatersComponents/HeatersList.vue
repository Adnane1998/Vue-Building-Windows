<template>
  <div class="windows-list pt-3">
    <heaters-list-item
      v-for="heater in heaters"
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
      heaters: []
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/heaters`);
    let heaters = response.data;
    this.heaters = heaters;
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
