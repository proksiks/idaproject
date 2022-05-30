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
            title="Наименование товара"
            placeholder="Введите наименование товара"
            :error="$v.form.fullname.$error"
            v-model="$v.form.fullname.$model"
            error-text="Поле является обязательным"
            @send="handlyInput"
          />
          <CustomTextarea
            class="add-card__item"
            title="Описание товара"
            placeholder="Введите описание товара"
          />
          <CustomInput
            class="add-card__item"
            required
            title="Ссылка на изображение товара"
            placeholder="Введите ссылку"
            :error="$v.form.link.$error"
            v-model="$v.form.link.$model"
            error-text="Поле является обязательным"
          />
          <CustomInput
            class="add-card__item"
            required
            title="Цена товара"
            placeholder="Введите цену"
            :error="$v.form.price.$error"
            v-model="$v.form.price.$model"
            error-text="Поле является обязательным"
          />
          <Button
            @click="addItem"
            class="add-card__btn"
            green
            :disabled="$v.form.$invalid"
          >
            Добавить товар
          </Button>
        </Box>
      </div>
      <div class="right">
        <div class="items">
          <Card
            v-for="card in cards"
            :key="card.id"
            :img="card.img"
            :title="card.title"
            :text="card.text"
            :price="formatPrice(card.price)"
          />
        </div>
      </div>
    </div>
    <Card />
  </main>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";
export default {
  name: "IndexPage",
  data() {
    return {
      disabled: false,
      name: "",
      card: {
        img: "",
        title: "",
        text: "",
        price: "",
      },
      cards: [
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          img: "/images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
      ],

      form: {
        fullname: "",
        link: "",
        price: "",
      },
      errors: {
        fullname: false,
        link: false,
        price: false,
      },
    };
  },
  validations() {
    return {
      form: {
        fullname: {
          required,
          minLength: minLength(4),
          serverValid: () => !this.errors.fullname,
        },
        link: {
          required,
          serverValid: () => !this.errors.link,
        },
        price: {
          required,
          serverValid: () => !this.errors.price,
        },
      },
    };
  },
  methods: {
    addItem() {
      console.log("123");
    },
    formatPrice(value) {
      return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
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
  top: 16px;
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
