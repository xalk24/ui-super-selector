<template>
<div class="selector__list" ref="list" tabindex="0" @keyup="onKeyPressed">
  <template v-if="$scopedSlots.item">
    <slot
        name="item"
        v-for="(item, i) in items"
        v-bind:item="item"
        v-bind:on="selectItem"
        v-bind="{inFocus: i === focusedItem}" />
  </template>
  <item v-else v-for="(item, i) in listItems"
        :item="item"
        :key="i"
        :in-focus="i === focusedItem"
        @click="selectItem(item)" />
</div>
</template>

<script>
import Item from './item'

export default {
  name: "list",
  components: { Item },
  props: {
    value: {require: true},
    items: [Array, Object],
    labelKey: {
      type: String,
      require: false,
      default: 'label'
    },
    valueKey: {
      type: String,
      require: false,
      default: 'value'
    }
  },
  data() {
    return {
      focusedItem: -1
    }
  },
  computed: {
    listItems() {
      if (Array.isArray(this.items)){
        if(typeof this.items[0] !== 'object') {
          return this.items.map((item) => {
            return {
              label: item,
              value: item
            }
          })
        } else {
          return this.items.map(item => {
            return {
              label: item[this.labelKey],
              value: item[this.valueKey]
            }
          })
        }
      }

      const itemsKeys = Object.keys(this.items)
      return itemsKeys.map((key) => {
        let label = typeof this.items[key] !== "object" ?
          this.items[key] :
          this.items[key].label !== undefined ? this.items[key].label : this.items[key][this.labelKey]
        return {
          label: label,
          value: key
        }
      })
    }
  },
  methods: {
    selectItem(event) {
      this.$emit('close')
      this.$emit('input', event)
    },
    goToElement(inc) {
      if(this.focusedItem + inc >= this.listItems.length) {
        this.focusedItem = 0
      } else if (this.focusedItem + inc < 0) {
        this.focusedItem = this.listItems.length - 1
      } else {
        this.focusedItem += inc
      }
    },
    onKeyPressed(event) {
      event.stopPropagation()
      switch (event.key){
        case 'ArrowUp' : this.goToElement(-1);break;
        case 'ArrowDown' : this.goToElement(1);break;
        case 'Enter' : this.selectItem(this.listItems[this.focusedItem].value);break;
        case 'Escape' : this.$emit('close');break;
      }
    }
  },
  mounted() {
    this.$refs.list.focus()
  }
}
</script>

<style lang="scss">
.selector__list{
  position: absolute;
  top: 100%;
  left: -1px;
  background: #61fff0;
  border-width: 0 1px 1px 1px;
  border-style: solid;
  border-color: #87b9b2;
  border-radius: 0 0 4px 4px;
  width: 100%;
  &:focus {
    outline: none;
  }
}
</style>
