<template v-if="filteredRows">
  <div class="windows-list pt-3">
    
       <input type="text"

         placeholder="Filter by Room"
         v-model="filter" />

  
  <hr>
 
  
    <rooms-list-item
      v-for="room in filteredRows"
      :room="room"
      :key="room.id"  
      @room-updated="updateRoom"
    >
    </rooms-list-item>
    

  
        <room-create-item>
        </room-create-item>

  </div>
</template>


<script>
import axios from 'axios';
import {API_HOST} from '../../config';


import RoomCreateItem from './RoomCreateItem';
import RoomsListItem from './RoomsListItem';

 
export default {
  components: {

    RoomCreateItem,
     RoomsListItem

  },
  name: 'RoomsList',
  data: function() {
    return {
      /* Initialize windows with an empty array, while waiting for actual data to be retrieved from the API */
      rooms: [],
       filter:'',
           rows: [
      { department: 'Accounting', employees: ['Bradley', 'Jones', 'Alvarado'] },
      { department: 'Human Resources', employees: ['Juarez', 'Banks', 'Smith'] },
      { department: 'Production', employees: ['Sweeney', 'Bartlett', 'Singh'] },
      { department: 'Research and Development', employees: ['Lambert', 'Williamson', 'Smith'] },
      { department: 'Sales and Marketing', employees: ['Prince', 'Townsend', 'Jones'] }
    ],
 

    }
  },
  
  created: async function() {
    let response_rooms = await axios.get(`${API_HOST}/api/rooms`);
    let rooms = response_rooms.data;
    this.rooms = rooms;
   
  
  },
  computed: {
  filteredRows() {
    return this.rooms.filter(row => {
       const names= row.name.toString().toLowerCase();
       const floors= row.floor.toString().toLowerCase();
   
      const searchTerm = this.filter.toLowerCase();

      return names.includes(searchTerm) ||
        floors.includes(searchTerm);
    });
  }
},
  
  methods: {

    updateRoom(newRoom) {
      /* Find the place of window objectw ith the same Id in the array, and replace it */
      let index = this.rooms.findIndex(room => room.id === newRoom.id);
      this.rooms.splice(index, 1, newRoom);
    }
  }
}
</script>
