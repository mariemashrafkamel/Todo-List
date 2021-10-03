<template>
  <div>
      <div v-for="(item,index) in items" :key="index">
        <list-item  :item="item"
                     class="item"
                     v-on:itemChanged="$emit('reloadlist')"
                     
         />
         
      </div>
  </div>
</template>

<script>
import listItem from "./listItem";

export default {
    //hya5od items de mn app.vue feha v-bind items
    props: ['items'],
    components: {
        listItem,
    },
    

};
</script>

<style scoped>
.item {
background: gray;
padding: 10px;
margin: auto;

}
</style>