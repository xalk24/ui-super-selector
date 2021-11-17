<template>
<div class="selector" :class="{selected: isOpen}">
  <div class="selector__selected-value">
    <template v-if="text">
      {{ text }}
    </template>
    <template v-else>
      <template v-if="$slots.default">
        <slot />
      </template>
      <template v-else>
        {{ placeholder }}
      </template>
    </template>
  </div>
  <div class="selector__show-btn" @click="isOpen = !isOpen">
    <chevron-icon :is-rotated="isOpen"/>
  </div>
  <list v-if="isOpen" :items="items" :value="value" @input="itemSelected" @close="isOpen=false">
    <template v-if="$scopedSlots.item" v-slot:item="{item, on, inFocus}">
      <slot name="item" v-bind="{item, on, inFocus}"/>
    </template>
  </list>
</div>
</template>

<script>
import ChevronIcon from "@/components/selector/chevron-icon";
import List from "@/components/selector/list";
export default {
  name: "selector",
  components: {List, ChevronIcon},
  props: {
    placeholder: {
      default: 'Select item'
    },
    items: [Array, Object],
    value: {
      require: true
    }
  },
  data() {
    return {
      isOpen: false,
      text: ''
    }
  },
  methods: {
    itemSelected(event) {
      this.text = event.label
      this.$emit('input', event.value)
    }
  }
}
</script>

<style lang="scss">
.selector {
  display: flex;
  width: 300px;
  background: #61fff0;
  border-width: 1px;
  border-style: solid;
  border-color: #87b9b2;
  border-radius: 4px;
  position: relative;
  &.selected {
    border-bottom-color: transparent;
    border-radius: 4px 4px 0 0;
  }
  &__selected-value {
    padding: 8px;
  }
  &__show-btn {
    display: flex;
    margin-left: auto;
    padding-right: 4px;
    cursor: pointer;
  }
}
</style>
