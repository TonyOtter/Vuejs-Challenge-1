
<template>
   <section class="board">
      <h2>{{title}}</h2>

      <draggable v-model="listArray" class="cards-area" group={groupName} >
         <transition-group>
            <div v-for="(element, index) in listArray"  :key="index" class="card-item" >
                  {{element.name}}
                  <img src="@/assets/img/delete-can.png" v-on:click="deleteElement(index)" />
            </div>
         </transition-group>
      </draggable>

      <div class="actions">
         <div class="group">
            <input type="text" placeholder="To-do name" v-model="itemName" />
            <button v-on:click="addItem()">Add new item</button>
         </div>
         <div class="group">
            <button v-on:click="sortItems()">Sort Alphabetically</button>
            <button v-on:click="deleteList()">Delete List</button>
         </div>
      </div>

   </section>
</template>

<script>
import draggable from 'vuedraggable';

export default {
   data() {
      return {
         itemName: "",
         listArray: []          
      }
   },
   props: {
      title: {
         type: String,
         required: true
      },
      arrayId: {
         type: Number,
         required: true         
      }
   },
   components: {
      draggable
   },
   methods: {
      deleteElement(id) {
         this.listArray.splice(id, 1);
      },
      deleteList() {
         this.$emit('deleteList', this.arrayId);
      },
      addItem() {
         if(this.itemName != "") {
            this.listArray.push({
               name: this.itemName
            })
         }
         this.itemName = "";
      },
      sortItems(arr) {
    		this.listArray= this.listArray.slice(0).sort((a, b) => a.name.toUpperCase() < b.name.toUpperCase() ? -1 : 1 );        
      }
   },
}
</script>