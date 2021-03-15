<template>
  <div id="app">
    <div class="shopping-place">
      <!-- SearchBar -->
      <SearchBar @searchFunc=" searchText = $event " />

      <!-- Shopping Items -->
      <ShoppingItems 
        @selectedItem="selectItem" 
        :searchingText="searchText" 
        :removedIndex="removedIndex"/>
    </div>
    <div class="calculate-place">
      <ShoppingCart :selectingItems="choosed" @deleteItem="deleteSelectedItem" />
    </div>
  </div>
</template>

<script>

import ShoppingCart  from './components/ShoppingCart.vue'
import SearchBar from './components/SearchBar.vue';
import ShoppingItems from './components/ShoppingItems.vue';

export default {
  name: 'App',
  /* Data */
  data() {
    return {
      choosed: [],
      searchText:'',
      removedIndex:null
    }
  },
  /* Components */
  components: {
    SearchBar,
    ShoppingItems,
    ShoppingCart
  },
  /* Emits */
  emits:['selectedItem','deleteItem','searchFunc'],
  /* Methods */
  methods: {
    selectItem(item){
      const hasItem=this.choosed.some(thing => thing.id == item.id);
      if(item && !hasItem){
        this.choosed.push(item);
      }
    },
    deleteSelectedItem(id){
      if(this.choosed.length){
        const deleteItemIndex = this.choosed.findIndex(item => item.id == id);
        this.choosed.splice(deleteItemIndex,1);

        this.removedIndex = { id };
      }
    },
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');

*{
  margin:0;
  padding:0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;  
}

button{
  cursor: pointer;
}

#app{
  background:#f1f1f1;
  height: 100vh;
  display: flex;
  overflow: hidden;
}

.shopping-place{
  padding: 1rem 0.5rem;
  min-height: 100vh;
  overflow-y: scroll;
  overflow-x:hidden ;
  width: 100%;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

@media screen and (max-width:400px) {
  html{
    font-size: 80%;
  }
}
</style>
