<template>
<li class="item flex items-center justify-between border-b-2">
  <div class="item-core flex items-center">
    <input class="item-control mr-2.5 cursor-pointer" type="checkbox" :checked="itemCheck" @click="$emit('update:itemCheck', $event.target.checked)">
    <h1 :class="`item-value ${itemCheck ? 'line-through italic' : ''}`" v-text="itemValue" />
  </div>
  <span class="item-action text-3xl transform rotate-45 cursor-pointer transition hover:scale-110 text-red-400" @click="$emit('removeItem')" >+</span>
</li>
</template>
<script>
export default {
  props: {
    itemValue: {
      type: String,
      required: true
    },
    itemCheck: {
      type: Boolean,
      required: true
    },
  }
}
</script>

