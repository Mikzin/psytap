<template>
  <div class="main">
    <base-container>
      <img src="./images/logo.jpg" alt="main photo" class="logo" />
      <h1>Корги Чуи</h1>
      <h2>@corgi_chewie</h2>
    </base-container>
    <base-container>
      <base-button>
        <a
          href="https://www.instagram.com/corgi_chewie"
          target="#blank"
          class="social-link"
        >
          <ion-icon name="logo-instagram"></ion-icon>
          Instagram</a
        >
      </base-button>
      <base-button>
        <a
          href="https://www.tiktok.com/@corgi_chewie"
          target="#blank"
          class="social-link"
        >
          <ion-icon name="logo-tiktok"></ion-icon>
          TikTok</a
        >
      </base-button>
      <base-button>
        <a
          href="https://www.youtube.com/@corgi_chewie"
          target="#blank"
          class="social-link"
        >
          <ion-icon name="logo-youtube"></ion-icon>
          Youtube</a
        >
      </base-button>
      <base-button>
        <a
          href="https://www.tinkoff.ru/cf/1RPjsmfRfHt"
          target="#blank"
          class="social-link"
        >
          <ion-icon name="card-outline"></ion-icon>
          Чуи на вкусняшку</a
        >
      </base-button>
    </base-container>
    <base-container>
      <the-footer></the-footer>
    </base-container>
  </div>
</template>

<script>
import TheFooter from './components/layout/TheFooter.vue';
import BaseContainer from './components/UI/BaseContainer.vue';
import BaseButton from './components/UI/BaseButton.vue';

export default {
  components: { TheFooter, BaseContainer, BaseButton },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  font-family: 'Inter', sans-serif;
  font-style: normal;
  color: #83807c;
  max-width: 100%;
  margin: 0 auto;
}

body {
  margin: 0;
  font-size: 12px;
}

.main {
  background-color: #ffead2;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.logo {
  width: 200px;
  border-radius: 50%;
}

.social-link {
  text-decoration: none;
  color: #dbdfea;
  width: 100%;
  display: flex;
  gap: 8px;
  align-items: center;
  justify-content: center;
}

h1,
h2 {
  margin: 8px 0 6px;
}
</style>
