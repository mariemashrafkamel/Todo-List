<template>
  <div class="item">
    <input type="checkbox" @change="updateCheck()" v-model="item.completed" />
    <span :class="[item.completed ? 'completed' : '', 'itemText']">
      {{ item.name }}
    </span>
    <button @click="removeItem()" class="trashcan">
      <font-awesome-icon icon="trash" />
    </button>
  </div>
</template>

<script>
export default {
  //hya5od el item mn el listView
  props: ["item"],
  methods: {
      updateCheck () {
          axios.put('api/item/'+this.item.id,{
              item:this.item
          })
          .then(response=> {
              if(response.status==200)
              {
                  this.$emit('itemChanged');
              }
          })
          .catch(error => {
              console.log(error);
          })
      },
      removeItem()
      {
          axios.delete('api/item/'+this.item.id)
          .then(response=> {
              if(response.status==200)
              {
                  this.$emit('itemChanged');
              }
          })
          .catch(error => {
              console.log(error);
          })
      }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
  color: rgb(241, 196, 184);
}
.itemText {
  width: 100%;
  margin-left: 20px;
}
.item {
  font-size: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.trashcan {
  background: gray;
  border: none;
  color: rgb(0, 0, 0);
  outline: none;
}
</style>