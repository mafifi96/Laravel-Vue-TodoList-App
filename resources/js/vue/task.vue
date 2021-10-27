<template>
<div>

    <div  v-for="(item, index) in items" :key="index" :class="[(item.completed) ? 'completed' : '' , 'task']" >
        {{item.name}} <input v-model="item.completed" style="float:right;" type="checkbox" v-keyup.enter=""  @change="update(item.id , item)" /><button class="delete" @click="remove(item.id)">x</button>
    </div>

</div>
</template>

<script>
export default {
    props : ['items'],
    methods : {
        update(id , item){

            axios.put("api/item/"+ id , {
item : item
            }).then(response =>{
                if(response.status == 200){

                    this.$emit("ref");
                 }

            }).catch(error=>{
                console.log(error.responseText);
            });

        },
        remove(id){
   axios.delete("api/item/"+ id).then(response =>{
                if(response.status == 200){
                    this.$emit("ref");
                }

            }).catch(error=>{
console.log(error);
            });

            }
    }

}
</script>

<style scoped>
 .task{
    margin: 5px 0;
    padding:3px 5px;
    background: #eee;

}
.completed{
    background: green;
    color:white;
    text-decoration: line-through;
}
button{
    float: right;
    cursor:pointer;
}
</style>
