<template>
    <div class="todo">
<h2 class="title">Todo List</h2>
<add v-on:ref="getall"></add>
<br>
<task :items="items" v-on:ref="getall"></task>
    </div>
</template>

<script>
import add from './add'
import task from './task'

export default {
components : {
    add,
    task
},
data : function() {
    return {
        items : []
    }
    },

    methods: {
        getall (){
            axios.get("api/items")
            .then(response => {

                    this.items = response.data;

            })
            .catch(error=>{
                console.log(error);
            });
        }
    },
    created (){
        this.getall();
    }
}

</script>
<style  scoped>
.todo{
    padding:5px;
    margin: 40px auto;
    width: 400px;
    border-radius: 5px;
    border: 1px solid #eee;
}
</style>
