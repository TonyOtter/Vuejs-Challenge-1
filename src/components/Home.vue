
<template>
    <div class="home wrapper">
        <h1>To-do App</h1>

            <draggable class="boards-area">
                <transition-group>
                <Board v-for="(list, index) in lists" 
                :key="index" 
                :title="list.listName" 
                groupName="todo" 
                v-on:deleteList="deleteList"
                :arrayId="index"        
                />
                </transition-group>
            </draggable>

        <div class="actions" >
            <div class="group">
                <input type="text" placeholder="List Name" v-model="newListName" />
                <button v-on:click="newList">Create New List</button>
            </div>
        </div>
    </div>
</template>

<script>
import draggable from 'vuedraggable';
import Board from './Board';

export default {
name: 'Home',
components: {
    draggable,
    Board
},
data() {
    return {
        lists: [
            {
                listName: "To-do list"
            }          
        ],
        newListName: "",
        currentList: 0
    } 
},
methods: {
    saveItem(itemDetails) {
        if(itemDetails.name != "") {
            this.lists[this.currentList].items.push(itemDetails);
            this.isModalOpen = false;
        }
    },
    newList() {
        if(this.newListName != "") {
            this.lists.push({
                listName: this.newListName,
                items: []
            })
            this.newListName = "";
        }
    },
    deleteList(id) {
        this.lists.splice(id, 1);
    },    
}

};
</script>

<style>
</style>
