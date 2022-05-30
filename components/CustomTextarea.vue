<template>
  <div class="custom-textarea">
    <div class="custom-textarea__title" :class="{ required }">{{ title }}</div>
    <textarea
      rows="6"
      class="custom-textarea__textarea"
      :placeholder="placeholder"
      @input="send"
    ></textarea>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    required: Boolean,
    placeholder: String,
  },
  methods: {
    send: function (e) {
      this.$emit("input", e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
.custom-textarea {
  // .custom-textarea__title
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
  // .custom-textarea__textarea
  &__textarea {
    display: block;
    width: 100%;
    resize: none;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    padding: 10px 16px;
    font-size: 0.75rem;
    line-height: 1.25;
    color: #b4b4b4;
    border: none;
    letter-spacing: -0.02em;
    transition: box-shadow 0.3s ease;
    &:focus {
      outline: none;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2);
    }
    &::placeholder {
      font-family: inherit;
      font-size: inherit;
      line-height: inherit;
      color: inherit;
      letter-spacing: -0.02em;
    }
  }
}
</style>
