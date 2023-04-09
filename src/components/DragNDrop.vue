<template>
    <div class="todo-list">
        <h2>DragNDrop Issue list</h2>
        <div class="drop-zone-list">
            <div class="to-do zone">
                <p>To-do</p>
                <div class="to-do drop-zone" @dragenter.prevent @dragover.prevent @drop="dropping($event, 1)">
                    <div v-for="item in getItem(1)" :key="item.id" class="drag-element" draggable="true"
                    @dragstart="startDrag($event, item)" :class="changeBG(1)">
                    {{ item.todo }}
                </div>
            </div>   
        </div> 
        
        <div class="checking zone">
            <p>Checking</p>
            <div class="to-do drop-zone" @dragenter.prevent @dragover.prevent @drop="dropping($event, 2)">
                <div v-for="item in getItem(2)" :key="item.id" class="drag-element" draggable="true"
                @dragstart="startDrag($event, item)" :class="changeBG(2)">
                {{ item.todo }}
                </div>
            </div>   
        </div>
    
        <div class="done zone">
            <p>Done</p>
            <div class="to-do drop-zone" @dragenter.prevent @dragover.prevent @drop="dropping($event, 3)">
                <div v-for="item in getItem(3)" :key="item.id" class="drag-element" draggable="true"
                @dragstart="startDrag($event, item)" :class="changeBG(3)">
            {{ item.todo }}
                </div>
            </div>   
        </div>
</div>
</div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup(){
        const items = ref([{id: 0, todo: 'Do homework', list: 1}, {id: 1, todo: 'Clean house', list: 1 }, {id: 2, todo: 'Make a shopping', list: 1}, {id: 3, todo: 'Read a book', list: 1}, {id: 4, todo: 'Learn new words', list: 1}]);
        
        function getItem(list){
            return items.value.filter(item => item.list === list);
        }
        
        function startDrag(event, item){
            event.target.style.background = "dodgerblue";
            event.dataTransfer.dropEffect = "move";
            event.dataTransfer.effectAllowed = "move";
            event.dataTransfer.setData("itemID", item.id);
        }
        
        function dropping(event, list){
            const itemId = event.dataTransfer.getData("itemID");
            items.value.forEach(item => {
                if (item.id == itemId) {
                    item.list = list;
                }
            });
        }
        
        function changeBG(list){
            const classMap = new Map(
                [
                    [1, 'default-bg'],
                    [2, 'checking-bg'],
                    [3, 'done-bg'],
                ]
            )

            return classMap.get(list);
        }

        return {
            items,
            getItem,
            startDrag,
            dropping,
            changeBG,
        }
    }   
}
</script>

<style>
.todo-list{
    display: flex;
    flex-direction: column;
    row-gap: 15px;
}

.drop-zone-list{
    flex-grow: 1;
    display: flex;
    flex-wrap: wrap;
    column-gap: 15px;
    padding: 15px;
    border-radius: 15px;
    box-shadow: 0 0 2px 2px lightblue;
    background-color: white;
}

.drop-zone{
    display: flex;
    flex-direction: column;
    row-gap: 5px;
    min-height: 100px;
}

.zone{
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    row-gap: 10px;
    width: calc(33.33333% - 15px);
}

.drag-element{
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    width: 100%;
    cursor: pointer;
    padding: 5px;
    border-radius: 5px;
}

.default-bg{
    background-color: slateblue;
}

.checking-bg{
    background-color: goldenrod;
}

.done-bg{
    background-color: green;
}

</style>