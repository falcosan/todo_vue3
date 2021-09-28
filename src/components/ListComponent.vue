<template>
<div class="list container max-w-5xl mx-auto mt-10 mb-0 overflow-hidden rounded font-mono bg-gray-100">
	<div class="flex flex-col bg-gray-200">
		<h1 class="list-title text-center mt-5 mb-2.5 text-3xl italic">todo today</h1>
      <Form @addItem="addItem" @clearAll="clearAll" v-model:input-value="newItem.val"/>
    </div>
    <ul class="list-items h-full py-2.5 px-5 overflow-y-scroll">
      <Item v-for="(item, index) in items" :class="`${index === 0 ? '' : 'mt-2.5'}`" :item-value="item.val" :key="`item-${index}`" v-model:item-check="item.checked" @removeItem="removeItem(index)"/>
    </ul>
</div>
</template>
<script>
import Form from "./FormComponent.vue";
import Item from "./ItemComponent.vue";
import { ref, onUpdated } from 'vue'
export default {
  components: { Form, Item },
  setup() {
    const newItem = ref({
      val: '',
      checked: false
     })
     const setItems = localStorage['storageItems'] ? JSON.parse(localStorage.getItem('storageItems')) : [];
     const items = ref(setItems)
     onUpdated(()=>{
       saveStorage()
     })
      function addItem () {
          if (newItem.value.val) {
              items.value.push(newItem.value)
              newItem.value = {
                val: '',
                checked: false
            }
            saveStorage();
          }
      }
    function saveStorage() {
        localStorage.setItem('storageItems', JSON.stringify(items.value))
    }
    function removeItem (key) {
        items.value.splice(key, 1)
    }
    function clearAll () {
			items.value = []
        newItem.value = {
        value: '',
        checked: false
      },
      localStorage.removeItem('storageItems');
		}
    return {
      newItem,
      items,
      addItem,
      removeItem,
      clearAll
      }
  }
};
</script>