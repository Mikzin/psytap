<template>
  <div class="main">
    <base-container>
      <img src="./images/logo.jpg" alt="main photo" class="logo" />
      <h1>Зинчук Михаил</h1>
      <h2>Психолог</h2>
      <h2>Специалист по клинической психологии</h2>
      <h2>Рационально-эмотивно-поведенческий (РЭПТ) консультант</h2>
    </base-container>
    <base-container>
      <div>
        <ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="chevron-down-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon>
      </div>
    </base-container>
    <base-container>
      <h2>Формат работы:</h2>
      <div class="work-info">
        <ion-icon name="laptop-outline" class="social-link icon"></ion-icon>
        <div class="work-info_block">
          <h3>Онлайн консультация</h3>
          <div class="work-info_text">
            из любой точки мира в Skype, WhatsApp, Telegram, GoogleMeet.
            <br />Длительность — <b>50 минут</b> <br />Стоимость —
            <b>2000 рублей</b>
          </div>
        </div>
      </div>
    </base-container>

    <base-container>
      <div>
        <ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="chevron-down-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon
        ><ion-icon name="remove-outline" class="icon-divider"></ion-icon>
      </div>
    </base-container>

    <base-container>
      <h2>Связаться со мной:</h2>
      <base-button>
        <a href="https://t.me/mik_zin" target="#blank" class="social-link">
          <ion-icon name="paper-plane-outline"></ion-icon>
          Telegram</a
        >
      </base-button>
      <base-button>
        <a href="https://wa.me/79675106752" target="#blank" class="social-link">
          <ion-icon name="logo-whatsapp"></ion-icon>
          WhatsApp</a
        >
      </base-button>
    </base-container>
    <base-container>
      <h2>Образование:</h2>
      <base-carousel></base-carousel>
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
import BaseCarousel from './components/UI/BaseCarousel.vue';

export default {
  components: {
    TheFooter,
    BaseContainer,
    BaseButton,
    BaseCarousel,
  },
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
  padding: 10px;
}

.logo {
  width: 200px;
  border-radius: 50%;
}

.social-link {
  text-decoration: none;
  color: #fff;
  width: 100%;
  display: flex;
  gap: 8px;
  align-items: center;
  justify-content: center;
}

h1 {
  margin: 8px 0 6px;
}

h2 {
  margin: 8px 0 0;
  text-align: center;
}

h3 {
  margin: 8px 0 0;
}

.icon {
  color: #83807c;
  width: 50px;
  height: 50px;
}

.work-info {
  display: flex;
  gap: 20px;
  align-items: center;
  justify-content: center;
}

.work-info_block {
  width: 50%;
}

.work-info_text {
  font-size: 14px;
}

.icon-divider {
  height: 18px;
  width: 18px;
}
</style>
