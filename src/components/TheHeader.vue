<template>
  <div class="header">
    <img
      src="@/assets/images/logo/agencia-eplus-n-logo.png"
      alt="Logo"
      class="header__logo"
    />
    <div class="header__items">
      <ul class="items">
        <li v-for="(item, i) in menuItems" :key="i" class="items__option">
          <span>{{ item.title }}</span>
        </li>
      </ul>
    </div>
    <div class="header__user-menu">
      <img
        src="@/assets/icons/search.svg"
        alt="User menu"
        class="user-menu__item hidden-in-mobile"
      />
      <img
        src="@/assets/icons/person.svg"
        alt="User menu"
        class="user-menu__item hidden-in-mobile"
      />
      <img
        src="@/assets/icons/shopping_cart.svg"
        alt="User menu"
        class="user-menu__item"
      />
      <img
        src="@/assets/icons/menu.svg"
        alt="User menu"
        class="user-menu__item hidden-in-desktop"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheHeader',
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
  height: 50px;
  padding: 8px;
  display: grid;
  align-content: center;
  box-shadow: 0 5px 5px rgba(0, 0, 0, 0.2);
  grid-template-columns: auto auto auto;
}

.header__logo {
  height: 35px;
}

.header__items {
  display: none;
}

.items__option {
  list-style: none;
  padding: 0 10px;
}

.items__option:last-child {
  font-weight: 600;
  color: yellowgreen;
}

.header__user-menu {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.user-menu__item {
  height: 20px;
  padding: 0 10px;
}

@media only screen and (min-width: 600px) {
  .header {
    height: 75px;
  }

  .header__logo {
    height: 50px;
  }

  .header__items {
    display: flex;
  }

  .items {
    display: flex;
    align-items: center;
  }

  .user-menu__item {
    height: 25px;
  }
}
</style>
