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
            :error="$v.form.title.$error"
            v-model="$v.form.title.$model"
            error-text="Поле является обязательным"
          />
          <CustomTextarea
            class="add-card__item"
            title="Описание товара"
            placeholder="Введите описание товара"
            v-model="$v.form.text.$model"
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
            type="number"
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
        <transition-group class="items" name="card" tag="div">
          <Card
            class="item"
            v-for="card in cards"
            :key="card.id"
            :img="card.img"
            :title="card.title"
            :text="card.text"
            :price="formatPrice(card.price)"
            @delete="deleteItem(card.id)"
          />
        </transition-group>
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
      cards: [
        {
          id: 1,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 2,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
      ],

      form: {
        title: "",
        link: "",
        text: "",
        price: "",
      },
      errors: {
        title: false,
        link: false,
        price: false,
        text: true,
      },
    };
  },
  validations() {
    return {
      form: {
        title: {
          required,
          minLength: minLength(4),
          serverValid: () => !this.errors.title,
        },
        link: {
          required,
          serverValid: () => !this.errors.link,
        },
        text: {
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
    addItem: function () {
      const card = {
        id: this.cards.length + 1,
        img: this.form.link,
        title: this.form.title,
        text: this.form.text,
        price: this.form.price,
      };
      this.cards.push(card);
    },
    deleteItem: function (cardId) {
      let cardToRemove = this.cards.find((card) => {
        return card.id === cardId;
      });
      let cardIndex = this.cards.indexOf(cardToRemove);
      this.cards.splice(cardIndex, 1);
    },
    formatPrice(value) {
      return value.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ");
    },
  },
};
</script>

<style lang="scss" scoped>
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
  position: relative;
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
.item {
  &::v-deep {
    transition: box-shadow 0.6s ease, transform 0.6s ease, opacity 0.6s ease;
  }
}
.head {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.card-enter,
.player-leave-to {
  opacity: 0;
}
.card-enter {
  transform: scale(1);
}
.card-leave-to {
  transform: scale(0) translateY(-100%);
}
.card-leave-active {
  width: 33%;
  position: absolute;
  @media (max-width: 1023px) {
    width: 50%;
  }
  @media (max-width: 480px) {
    width: 100%;
  }
}
</style>
