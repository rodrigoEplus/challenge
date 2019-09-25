<template>
  <div class="header">
    <div class="header__wrapper">
      <div class="header__logo">
        <img
          src="@/assets/images/logo/agencia-eplus-n-logo.png"
          alt="Logo"
          class="header__logo__image"
        />
      </div>
      <div class="header__items hidden-in-mobile">
        <ul class="items">
          <li v-for="(item, i) in menuItems" :key="i" class="items__option">
            <span>{{ item.title }}</span>
          </li>
        </ul>
      </div>
      <div class="header__user-menu">
        <div class="header__user-menu__item hidden-in-mobile">
          <img src="@/assets/icons/search.svg" alt="User menu" />
        </div>
        <div class="header__user-menu__item hidden-in-mobile">
          <img src="@/assets/icons/person.svg" alt="User menu" />
        </div>
        <!-- <img
        src="@/assets/icons/shopping_cart.svg"
        alt="User menu"
        class="header__user-menu__item"
      /> -->
        <div class="header__user-menu__item">
          <shopping-cart />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ShoppingCart from '@/components/ShoppingCart'

export default {
  name: 'TheHeader',
  components: { ShoppingCart },
  data() {
    return {
      menuItems: [
        {
          title: 'Notebooks',
          path: 'menu1',
        },
        {
          title: 'Impressoras',
          path: 'menu2',
        },
        {
          title: 'Smartphones',
          path: 'menu2',
        },
        {
          title: 'Livros',
          path: 'menu2',
        },
        {
          title: 'Ofertas',
          path: 'menu2',
        },
      ],
    }
  },
}
</script>

<style scoped>
.header {
  box-shadow: 0 5px 5px rgba(0, 0, 0, 0.2);
}

.header__wrapper {
  height: 50px;
  max-width: 1440px;
  margin: 0 auto;
  padding: 0 8px;
  display: flex;
}

.header__logo {
  height: 35px;
  align-self: center;
  flex-grow: 1;
}

.header__logo__image {
  height: 100%;
}

.header__items {
  flex-grow: 1;
}

.items__option {
  list-style: none;
  padding: 0 10px;
}

.header__user-menu {
  display: flex;
  justify-content: flex-end;
  flex-grow: 1;
}

.header__user-menu__item {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
}

@media only screen and (min-width: 1024px) {
  .header__wrapper {
    height: 75px;
    padding: 0;
  }

  .header__logo {
    height: 50px;
  }

  .header__items {
    display: flex;
    justify-content: center;
  }

  .items {
    display: flex;
    align-items: center;
  }

  .header__user-menu__item {
    width: 70px;
  }
}
</style>
