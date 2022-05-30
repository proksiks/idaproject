<template>
  <main class="main">
    <div class="head">
      <Title>Добавление товара</Title>
      <div class="select">
        <multiselect
          v-model="value"
          :options="options"
          :searchable="false"
          :close-on-select="false"
          :show-labels="false"
          placeholder="По умолчанию"
        ></multiselect>
      </div>
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

      value: "По умолчанию",
      options: [
        "По умолчанию",
        "По наименованию",
        "По цене (от меньшего к большему)",
        "По цене (от большего к меньшему)",
      ],
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
        {
          id: 3,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 4,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 5,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 6,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 7,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 8,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 9,
          img: "images/card/img.jpg",
          title: "Наименование товара",
          text: "Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк",
          price: "10000",
        },
        {
          id: 10,
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
        text: false,
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
          serverValid: () => !this.errors.text,
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

<style lang="scss">
.head {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 14px;
}
.add-card {
  padding: 20px 24px 24px 24px;
  position: sticky;
  top: 16px;
  @media (max-width: 480px) {
    padding: 16px;
  }
  &__item {
    & + & {
      margin-top: 16px;
    }
    &:nth-child(3) {
      margin-top: 8px;
    }
    &:nth-child(4) {
      margin-top: 10px;
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
.multiselect {
  min-width: 122px;
  width: 100%;
  min-height: 38px;
  &__tags {
    display: flex;
    align-items: center;
    padding: 10px 26px 11px 16px;
    background: #fffefb;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    min-height: auto;
  }
  &__single {
    padding: 0;
    margin: 0;
    font-size: 0.75rem;
    line-height: 1.25;
    color: #b4b4b4;
    min-height: auto;
    background: #fffefb;
  }
  &__select {
    width: 38px;
    height: 100%;
    right: 0;
    top: 0;
    &::before {
      position: absolute;
      width: 5px;
      height: 5px;
      border: 1px solid #b4b4b4;
      margin: 0;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%) rotate(45deg);
    }
    &::after {
      content: "";
      background: #ffffff;
      position: absolute;
      width: 5px;
      height: 5px;
      margin: 0;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -90%) rotate(45deg);
    }
  }
  &__input {
    padding: 0;
    margin: 0;
    font-size: 0.75rem;
    line-height: 1.25;
    color: #b4b4b4;
    background: #fffefb;
    &::placeholder {
      font-family: inherit;
      font-size: inherit;
      font-weight: inherit;
      color: inherit;
    }
  }
  &__option {
    padding: 5px;
    margin: 0;
    font-size: 0.75rem;
    line-height: 1.25;
    color: #b4b4b4;
    background: #fffefb;
    min-height: auto;
    &--highlight {
      background: #b8b5ae;
      color: #ffffff;
    }
  }
  &__placeholder {
    padding: 0;
    margin: 0;
    font-size: 0.75rem;
    line-height: 1.25;
    color: #b4b4b4;
    background: #fffefb;
    min-height: auto;
  }
}

// animation cards
.card-enter,
.card-leave-to {
  opacity: 0;
}
.card-enter {
  transform: translateY(10%);
}
.card-leave-to {
  transform: translateY(-100%);
}
.card-leave-active {
  position: absolute;
  width: 32%;
  z-index: 0;
  @media (max-width: 1023px) {
    width: 50%;
  }
  @media (max-width: 480px) {
    width: 100%;
  }
}
</style>
