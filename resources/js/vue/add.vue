<template>
<div class="add">
<input @keyup.enter="add" type="text" v-model="item.name" placeholder="Enter New Task..">
<button @click="add">Add</button>
</div>
</template>

<script>
export default {
data : function ()
{
    return {
        item :{
            name : ""
        }
    }
},
methods : {
    add : function(){
        axios.post("api/item/store" , {
            item : this.item
        }).then(response=>{
            if(response.status == 201)
            {
                this.item.name = "";
                this.$emit("ref");
                console.log("saved");
            }

        }).catch(error=>{
            console.log(error);
        });
    }
}


}
</script>

<style scoped>
.add{
    padding: 10px 0;
    width: 100%;
}
 input {
    padding:5px;
    display: inline;

}
button{

    border: none;
    padding:5px;
    color:#fff;
    background: rgb(21, 250, 4);
    outline: none;
    cursor: pointer;
}
</style>
