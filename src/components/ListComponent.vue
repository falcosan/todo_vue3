<template>
<div class="list container max-w-5xl mx-auto mt-10 mb-0 overflow-hidden rounded font-mono bg-gray-100">
	<div class="flex flex-col bg-gray-200">
		<h1 class="list-title text-center mt-5 mb-2.5 text-3xl italic">todo today</h1>
      <Form @addItem="addItem" @clearAll="clearAll" v-model:input-value="newItem.value"/>
    </div>
    <ul class="list-items h-full py-2.5 px-5 overflow-y-scroll">
      <Item v-for="(item, index) in items" :class="`${index === 0 ? '' : 'mt-2.5'}`" :item-value="item.value" :key="`item-${index}`" v-model:item-check="item.checked" @removeItem="removeItem(index)"/>
    </ul>
</div>
</template>
<script>
import Form from "./FormComponent.vue";
import Item from "./ItemComponent.vue";
export default {
  components: { Form, Item },
  data() {
    return { 
      newItem: {
        value: '',
        checked: false
      },
      items: []
    };
  },
  mounted(){
    localStorage['storageItems'] ? this.items = JSON.parse(localStorage.getItem('storageItems')) : []
  },
  updated(){
   localStorage.setItem('storageItems', JSON.stringify(this.items))
  },
  methods: {
		addItem () {
      if (this.newItem.value) {
        this.items.push(this.newItem)
        this.newItem = {
        value: '',
        checked: false
      }
      }
		},
    removeItem (key) {
      this.items.splice(key, 1)
		},
		clearAll () {
			this.items = []
        this.newItem = {
        value: '',
        checked: false
      },
      localStorage.removeItem('storageItems');
		}
	}
};
</script>