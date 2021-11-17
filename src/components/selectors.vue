<template>
<div class="view">
  <div class="text">{{ simpleValue }}</div>
  <selector v-model="simpleValue" :items="simpleItems">
    <b>Sel</b>
  </selector>
  <selector :items="slotItems">
    <template v-slot:item="{on, item, inFocus}">
      <li @click="on({value: item.value, label: item.label})" :class="{focused: inFocus}">
        <span :style="{color: item.color}">{{item.label}}</span>
      </li>
    </template>
  </selector>
  <select>
    <option>op1</option>
    <option>op2</option>
  </select>
</div>
</template>

<script>
import Selector from "@/components/selector";
export default {
  name: "selectors",
  components: {Selector},
  data() {
    return {
      simpleValue: '',
      simpleItems: ['Option 1', 'Option 2', 'Option 3'],
      slotItems: [
        {
          label: 'Option red',
          color: 'red',
          value: '1'
        },
        {
          label: 'Option red',
          color: 'red',
          value: '1'
        }
      ]
    }
  }
}
</script>

<style lang="scss">
.view{
  display: flex;
  width: 80%;
  padding: 10px;
  margin: 20px auto;
  border: 4px solid #2c3e50;
  li {
    &.focused {
      text-decoration: underline;
    }
  }
}
</style>
