<template>
  <div class="custom-input">
    <div class="custom-input__title" :class="{ required }">{{ title }}</div>
    <input class="custom-input__input" type="text" :placeholder="placeholder" />
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    required: Boolean,
    placeholder: String,
  },
};
</script>

<style lang="scss" scoped>
@import "~/assets/styles/scss/_vars.scss";
.custom-input {

  // .custom-input__title
  &__title {
    position: relative;
    font-family: "Source Sans Pro";
    font-weight: 400;
    font-size: 0.625rem;
    line-height: 1.3;
    letter-spacing: -0.02em;
    color: #49485e;
    margin-bottom: 4px;
  }

  // .custom-input__input
  &__input {
    display: block;
    width: 100%;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    font-size: 0.75rem;
    line-height: 1.25;
    letter-spacing: -0.02em;
    color: $text-color;
    border: none;
    transition: box-shadow 0.3s ease;
    &:focus {
      outline: none;
      box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
    }
    &::placeholder {
      font-family: inherit;
      font-size: inherit;
      line-height: inherit;
      color: #b4b4b4;
    }
  }
}
</style>
