<template>
<div class="form grid auto-cols-fr shadow-md">
	<input :class="`form-input col-start-1 col-end-3 m-5 p-2.5 rounded ${valuePassed ? '' : 'bg-red-200'}`" 
        type="text" 
        placeholder="something to do" 
        :value="inputValue"
        @keyup="checkItem"
        @input="$emit('update:inputValue', $event.target.value)"
        @keypress.enter="addItem()"
	>
        <button class="form-add row-start-2 row-end-2 col-start-1 col-end-1 m-2.5 p-2.5 rounded transition hover:shadow-md hover:bg-opacity-90 bg-gray-500 text-white" 
        type="button"
        @click="addItem()"
                >
            add
			</button>
        <button class="form-cancel row-start-2 row-end-2 col-start-2 col-end-2 m-2.5 p-2.5 rounded hover:shadow-md hover:bg-opacity-90 bg-gray-400 text-white" 
        type="button"
        @click="$emit('clearAll')"
        >
			clear
			</button>
		</div>
</template>
<script>
export default {
props: {
    inputValue: {
      type: String,
      default: ''
    }
},
data(){
    return{
        valuePassed: true
    }
},
methods:{
checkItem(){
    if(!this.inputValue){
        this.valuePassed = false
    } else {
        this.valuePassed = true
    }
        },
        addItem(){
            this.checkItem()
            this.$emit('addItem')
        }
    }
}
</script>

