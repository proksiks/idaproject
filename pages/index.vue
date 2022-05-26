<template>
  <main class="main">
    <div class="head">
      <Title>Добавление товара</Title>
      <div class="select">По умолчанию</div>
    </div>
    <div class="wrapper">
      <div class="left">
        <Box class="add-card">
          <CustomInput
            class="add-card__item"
            required
            title="Наименование товара *"
            placeholder="Введите наименование товара"
          />
          <CustomTextarea
            class="add-card__item"
            required
            title="Описание товара"
            placeholder="Введите описание товара"
          />
          <CustomInput
            class="add-card__item"
            required
            title="Ссылка на изображение товара *"
            placeholder="Введите ссылку"
          />
          <CustomInput
            class="add-card__item"
            required
            title="Цена товара *"
            placeholder="Введите цену"
          />
          <Button
            class="add-card__btn"
            @click="alert"
            green
            :disabled="disabled"
          >
            Добавить товар
          </Button>
        </Box>
      </div>
      <div class="right">
        <div class="items">
          <Card v-for="card in cards" :key="card.id" :info="card" />
        </div>
      </div>
    </div>
    <Card />
  </main>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      disabled: false,

      cards: [
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10 000",
        },
      ],
    };
  },
  methods: {
    alert() {
      this.disabled = !this.disabled;
    },
  },
};
</script>

<style lang="scss">
.head {
  margin-bottom: 16px;
}
.add-card {
  padding: 24px;
  position: sticky;
  top: 20px;
  @media (max-width: 480px) {
    padding: 16px;
  }
  &__item {
    & + & {
      margin-top: 16px;
    }
  }
  &__btn {
    display: block;
    width: 100%;
    margin-top: 24px;
  }
}
.wrapper {
  display: grid;
  grid-template-columns: 332px 1fr;
  gap: 16px;
  @media (max-width: 1280px) {
    grid-template-columns: 1fr 3fr;
  }
  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
}
.left {
  min-width: 240px;
}
.items {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  @media (max-width: 1023px) {
    grid-template-columns: 1fr 1fr;
  }
  @media (max-width: 480px) {
    grid-template-columns: 1fr;
  }
}
.head {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
