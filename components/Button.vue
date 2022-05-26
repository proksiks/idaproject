<template>
  <button class="btn" :class="{ disabled, green }" @click="$emit('click')">
    <slot />
  </button>
</template>

<script>
export default {
  props: {
    green: Boolean,
    disabled: Boolean,
  },
};
</script>

<style lang="scss" scoped>
.btn {
  font-family: "Inter", sans-serif;
  cursor: pointer;
  border: none;
  background: none;
  padding: 10px 20px;
  text-align: center;
  border-radius: 10px;
  transition: box-shadow 0.3s ease, background 0.3s ease, color 0.3s ease;
  font-weight: 600;
  font-size: 12px;
  line-height: 15px;
  letter-spacing: -0.02em;

  //.btn.green
  &.green {
    color: #ffffff;
    background: #7bae73;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  }

  //.btn.disabled
  &.disabled {
    cursor: auto;
    background: #eeeeee;
    box-shadow: none;
    color: #b4b4b4;
  }

  &:focus {
    outline: none;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  }
}
</style>
