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
      <a class="nav-link "  aria-disabled="true">Rooms</a>
    </li>
  </ul>
  <template v-if="isWindowExpanded">
     <windows-list></windows-list>
    </template>
      <template v-if="isHeaterExpanded">
     <heaters-list></heaters-list>
    </template>
 </div>
</template>


<script>
import WindowsList from './WindowsComponents/WindowsList.vue';
import HeatersList from './HeatersComponents/HeatersList.vue';
export default {
  name: 'MainNavigation',
    components: {
  
    WindowsList,
    HeatersList,
  },
    data: function() {
    return {
      isWindowExpanded: false,
        isHeaterExpanded: false
    }
  },
   methods: {
    toggleWindowExpand() {
      this.isWindowExpanded = !this.isWindowExpanded;
      this.isHeaterExpanded = false;
    },
     toggleHeaterExpand() {
      this.isHeaterExpanded = !this.isHeaterExpanded;
       this.isWindowExpanded = false;
    },
}
}
</script>
