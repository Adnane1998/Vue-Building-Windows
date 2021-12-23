<template>
  <div class="window border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
  
      <div class="room-name fw-bold pe-3">{{room.name}} </div>
      <div class="room-floor fw-bold pe-3">floor {{room.floor}} </div>
       <div class="room-name fw-bold pe-3">Current temperature{{room.ct}}</div>
          <div class="room-name fw-bold pe-3">Target temperature{{room.tt}}</div>



      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <div class="details d-flex">
        <button type="button" class="btn btn-secondary me-2" @click="switchWindows">Switch Windows Status</button>
        <button type="button" class="btn btn-primary me-2" @click="switchHeaters">Switch Heaters Status</button>
        <button type="button" class="btn btn-danger " @click="deleteRoom">Delete window</button>

      </div>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../../config';

export default {
  name: 'RoomsListItem',
  props: ['room'],
  data: function() {
    return {
      isExpanded: false,
 
  
        
    }
  }, 
 

  methods: {
    toggleExpand() {
  
      this.isExpanded = !this.isExpanded;
      for(let i=0;i<this.windows.length;i++)
    {
 if(this.windows[i]["roomId"]==this.room.id)
 {
  this.room_windows[i]= this.windows[i]["windowStatus"]
  
 }

    }},
    async switchWindows() {
     await axios.put(`${API_HOST}/api/windows/${this.room.id}/switch`);
    },
      async switchHeaters() {
     await axios.put(`${API_HOST}/api/heaters/${this.room.id}/switch`);
    },
               
     async deleteRoom() {
       console.log(this.room.id);
   await axios.delete(`${API_HOST}/api/rooms/${this.room.id}`);
    window.location.reload();



     
    }
  }
}
</script>

<style lang="scss" scoped>

.open-status {
  .icon {
    position: relative;
  }

  &.open {
    color: #198754;
    .icon {
      font-size: 12px;
      top: -3px;
    }
  }

  &.closed {
    color: #dc3545;
  }
}

.window {
  .top-row {
    cursor: pointer;
  }
}
</style>
