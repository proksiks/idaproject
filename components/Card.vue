<template>
  <Box class="card" v-if="img && title">
    <div class="card__img">
      <img :src="img" :alt="img" />
    </div>
    <div class="card__content">
      <SubTitle>{{ title }}</SubTitle>
      <p class="card__text">{{ text }}</p>
      <div class="card__price">{{ price }} руб.</div>
    </div>
    <button class="card__delete" @click="$emit('delete')">
      <img src="/images/icons/delete.svg" alt="" />
    </button>
  </Box>
</template>

<script>
export default {
  props: {
    img: String,
    title: String,
    text: String,
    price: String,
  },
};
</script>

<style lang="scss" scoped>
@import "~/assets/styles/scss/_vars.scss";
.card {
  position: relative;
  border-radius: 4px;
  &:hover {
    .card__delete {
      opacity: 1;
      transform: translateY(0);
    }
  }
  //.card__img
  &__img {
    position: relative;
    padding-bottom: 60.1%;
    img {
      position: absolute;
      left: 0;
      top: 0;
      width: 100%;
      height: 100%;
      display: block;
      object-fit: cover;
      border-radius: 4px 4px 0 0;
    }
  }
  //.card__content
  &__content {
    display: flex;
    flex-direction: column;
    padding: 16px 16px 23px 16px;
    border-radius: 0 0 4px 4px;
    min-height: 223px;
  }
  //.card__price
  &__price {
    font-weight: 600;
    font-size: 1.5rem;
    line-height: 1.25;
    margin-top: auto;
  }
  //.card__delete
  &__delete {
    cursor: pointer;
    border: none;
    margin: 0;
    padding: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    right: -8px;
    top: -8px;
    width: 32px;
    height: 32px;
    background: $red-color;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    opacity: 0;
    transform: translateY(-5px);
    transition: opacity 0.3s ease, transform 0.3s ease, background 0.3s ease;
    &:hover {
      background: darken($red-color, 5);
    }
    &:active {
      background: darken($red-color, 10);
    }
  }
}
</style>
