<template>
  <div class="custom-input" :class="{ 'custom-input_error': error }">
    <div class="custom-input__title" :class="{ required }">{{ title }}</div>
    <input
      class="custom-input__input"
      :placeholder="placeholder"
      :required="required"
      :name="name"
      :value="value"
      :type="type"
      @input="send"
    />
    <span :class="{ 'custom-input__error-text': errorText }">
      {{ errorText }}
    </span>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    name: String,
    required: Boolean,
    placeholder: String,
    value: String,
    errorText: String,
    type: {
      type: String,
      default: "text",
    },
    error: Boolean,
  },
  methods: {
    send: function (e) {
      this.$emit("input", e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~/assets/styles/scss/_vars.scss";
.custom-input {
  position: relative;
  // .custom-input__title
  &__title {
    position: relative;
    display: inline-block;
    font-family: "Source Sans Pro";
    font-weight: 400;
    font-size: 0.625rem;
    line-height: 1.3;
    letter-spacing: -0.02em;
    color: #49485e;
    margin-bottom: 4px;
    &::before {
      content: "";
      position: absolute;
      right: -4px;
      top: 0;
      width: 4px;
      height: 4px;
      border-radius: 100%;
      background: $red-color;
    }
  }
  // .custom-input_error
  &_error {
    .custom-input__input {
      border: 1px solid $red-color;
    }
    .custom-input__error-text {
      opacity: 1;
      visibility: visible;
      transform: translateY(0);
    }
  }
  // .custom-input__error-text
  &__error-text {
    position: absolute;
    bottom: -14px;
    left: 0;
    width: 100%;
    font-size: 0.5rem;
    line-height: 1.25;
    letter-spacing: -0.02em;
    color: $red-color;
    opacity: 0;
    visibility: hidden;
    transform: translateY(-5px);
    transition: transform 0.3s ease, visibility 0.3s ease, opacity 0.3s ease;
  }

  // .custom-input__input
  &__input {
    display: block;
    width: 100%;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border: 1px solid transparent;
    border-radius: 4px;
    padding: 9px 15px 10px 15px;
    font-size: 0.75rem;
    line-height: 1.25;
    letter-spacing: -0.02em;
    color: $text-color;
    transition: box-shadow 0.3s ease, 0.3s ease;
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
