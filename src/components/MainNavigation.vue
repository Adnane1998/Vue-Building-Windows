<template>
 <div class="window border border-secondary rounded p-2 mb-2" >
  <ul class="nav nav-tabs">
    <li class="nav-item">
      <a class="nav-link " aria-current="page" @click="toggleWindowExpand" >Windows</a>
    </li>
     <li class="nav-item">
      <a class="nav-link "   @click="toggleHeaterExpand"  >Heaters</a>
    </li>
    <li class="nav-item">
      <a class="nav-link "   @click="toggleRoomExpand">Rooms</a>
    </li>
  </ul>
  <template v-if="isWindowExpanded">
     <windows-list></windows-list>
    </template>
      <template v-if="isHeaterExpanded">
     <heaters-list></heaters-list>
    </template>
      <template v-if="isRoomExpanded">
     <rooms-list></rooms-list>
    </template>
 </div>
</template>


<script>
import WindowsList from './WindowsComponents/WindowsList.vue';
import HeatersList from './HeatersComponents/HeatersList.vue';
import RoomsList from './RoomsComponents/RoomsList.vue';
export default {
  name: 'MainNavigation',
    components: {
  RoomsList,
    WindowsList,
    HeatersList,
  },
    data: function() {
    return {
      isWindowExpanded: false,
        isHeaterExpanded: false,
         isRoomExpanded: false
    }
  },
   methods: {
    toggleWindowExpand() {
      this.isWindowExpanded = !this.isWindowExpanded;
      this.isHeaterExpanded = false;
       this.isRoomExpanded = false;
      
    },
     toggleRoomExpand() {
      this.isRoomExpanded = !this.isRoomExpanded;
      this.isHeaterExpanded = false;
       this.isWindowExpanded = false;
    },
     toggleHeaterExpand() {
      this.isHeaterExpanded = !this.isHeaterExpanded;
       this.isWindowExpanded = false;
        this.isRoomExpanded = false;
    },
}
}
</script>
