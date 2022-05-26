<template>
  <div class="sub-title"><slot /></div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "~/assets/styles/scss/_vars.scss";
.sub-title {
  font-weight: 600;
  font-size: 1.25rem;
  line-height: 1.25;
}
</style>
