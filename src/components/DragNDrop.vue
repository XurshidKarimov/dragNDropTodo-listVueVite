<template>
    
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
        
        return {
            items,
            getItem,
            startDrag,
            dropping,
        }
    }   
}
</script>

<style>

</style>