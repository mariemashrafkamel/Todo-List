<template>
  <div class="addItem">
     <input type="text"   v-model="item.name"  v-on:keyup.enter="onEnter" />
     <font-awesome-icon 
          icon="plus-square"
          @click="addItem()"
         
          :class="[ item.name ? 'active' : 'inactive' , 'plus' ]"
     />
  </div>
</template>

<script>
export default {
    data: function ()
    {
        return {
            item: {
                name:""
            }
        }
    },
    methods: {
        addItem()
        {
            if(this.item.name=='')
            {
                return ;
            }
            else
            {
                axios.post('api/item/store',
                {
                    item:this.item
                })
                .then(response => {
                    if(response.status==201)
                    {
                        this.item.name="";
                    }
                })
                .catch(error => {
                    console.log(error);
                })
            }

           this.$emit('reloadlist');
            
        },
        onEnter:function()
        {
            if(this.item.name=='')
            {
                return ;
            }
            else
            {
                axios.post('api/item/store',
                {
                    item:this.item
                })
                .then(response => {
                    if(response.status==201)
                    {
                        this.item.name="";
                    }
                })
                .catch(error => {
                    console.log(error);
                })
            }

           this.$emit('reloadlist');

        }

    },
};
</script>


<style scoped>
.addItem{
display: flex;
justify-content: center;
align-items: center;
margin: auto;
}
input{
margin: 10px;
border: 0px;
outline: none;
width: 100%;
padding: 10px;

}
.plus{
font-size:20px;
}
.active {
color: rgb(28, 119, 89);
}
.inactive{
color: blue;
}



</style>