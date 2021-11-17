<template>
<div class="selector__item"
     :class="{focused: inFocus}"
     @click="$emit('click', {label: item.label, value: item.value})">
  {{ item.label }}
</div>
</template>

<script>
export default {
  name: "item",
  props: {
    item: Object,
    inFocus: Boolean
  },
  data() {
    return {
      value: this.item.value
    }
  }
}
</script>

<style lang="scss">
.selector__item {
  display: flex;
  align-items: center;
  height: 30px;
  padding: 4px;
  background: #61fff0;
  cursor: pointer;
  &.focused{
    background: #0ff5df;
  }
  &:hover {
     background: #0ff5df;
  }
}
</style>
