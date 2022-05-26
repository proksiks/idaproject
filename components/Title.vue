<template>
  <div class="title"><slot /></div>
</template>

<script>
export default {};
</script>

<style lang="scss" scoped>
@import "~/assets/styles/scss/_vars.scss";
.title {
  font-weight: 600;
  font-size: 1.75rem;
  line-height: 1.25;
  @media (max-width: 768px) {
    font-size: 1.3rem;
  }
}
</style>
