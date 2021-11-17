<template>
  <svg width="24px" class="chevron-icon" :class="{rotated: isRotated}" viewBox="0 0 32 32" xmlns="http://www.w3.org/2000/svg">
    <g data-name="Layer 2" id="Layer_2">
      <path
          d="M16,21a1,1,0,0,1-.71-.29l-8-8a1,1,0,1,1,1.42-1.42L16,18.59l7.29-7.3a1,1,0,0,1,1.42,1.42l-8,8A1,1,0,0,1,16,21Z"/>
    </g>
    <g id="frame">
      <rect class="cls-1" height="32" width="32"/>
    </g>
  </svg>
</template>

<script>
export default {
  name: "chevron-icon",
  props: {
    isRotated: Boolean
  }
}
</script>

<style lang="scss">
.cls-1{
  fill: none;
}

.chevron-icon {
  transition-duration: 0.5s;

  &.rotated {
    transform: rotate(-180deg);
  }
}
</style>
