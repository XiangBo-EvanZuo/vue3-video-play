<template>
  <!-- <svg class="d-icon" :style="iconSize" aria-hidden="true">
    <use :xlink:href="`#${icon}`" />
  </svg>-->
  <i class="d-icon iconfont" :class="icon" :style="iconSize"></i>
</template>
<script>

export default {
  name: "d-icon"
}
</script>
<script setup>
import { computed } from 'vue'
// const emits = defineEmits('click')
const props = defineProps({
  icon: String,
  size: [Number, String],
})
const iconSize = computed(() => {
  let size = /^\d+$/.test(props.size) ? props.size + "px" : props.size
  return { fontSize: size };
})

</script>
<style lang = "less" scoped >
@import "../style/iconfont.css";
.d-icon {
  display: inline-block;
  cursor: pointer;
  overflow: hidden;
}
</style>
