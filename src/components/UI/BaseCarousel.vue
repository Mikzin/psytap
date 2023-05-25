<template>
  <div class="slider">
    <button @click="previousSlide" class="slider__button" v-if="countWidth()">
      <ion-icon name="chevron-back-outline"></ion-icon>
    </button>
    <img
      :src="currentSlide"
      alt="Slide"
      class="carousel__image"
      @mouseenter="stopSlideShow"
      @mouseleave="startSlideShow"
      @click="openFullScreen"
    />
    <button
      @click="nextSlide, stopSlideShow"
      class="slider__button"
      v-if="countWidth()"
    >
      <ion-icon name="chevron-forward-outline"></ion-icon>
    </button>
  </div>

  <div class="fullscreen-overlay" v-if="isFullScreen" @click="closeFullScreen">
    <img :src="currentSlide" alt="Slide" class="fullscreen-image" />
  </div>
</template>

<script>
import image1 from '../../images/1.jpg';
import image2 from '../../images/2.jpg';
import image3 from '../../images/3.jpg';
import image4 from '../../images/4.jpg';
import image5 from '../../images/5.jpg';
import image6 from '../../images/6.jpg';
import image7 from '../../images/7.jpg';
import image8 from '../../images/8.jpg';
import image9 from '../../images/9.jpg';
import image10 from '../../images/10.jpg';
import image11 from '../../images/11.jpg';
import image12 from '../../images/12.jpg';

export default {
  data() {
    return {
      slides: [
        image6,
        image7,
        image8,
        image1,
        image2,
        image3,
        image4,
        image5,
        image9,
        image11,
        image12,
        image10,
      ],
      currentIndex: 0,
      isHovered: false,
      isFullScreen: false,
    };
  },
  computed: {
    currentSlide() {
      return this.slides[this.currentIndex];
    },
  },
  methods: {
    previousSlide() {
      if (!this.isHovered && !this.isFullScreen) {
        this.currentIndex =
          (this.currentIndex - 1 + this.slides.length) % this.slides.length;
      }
    },
    nextSlide() {
      if (!this.isHovered && !this.isFullScreen) {
        this.currentIndex = (this.currentIndex + 1) % this.slides.length;
      }
    },
    startSlideShow() {
      if (!this.isHovered && !this.isFullScreen) {
        this.slideShowInterval = setInterval(() => {
          this.nextSlide();
        }, 3000);
      }
    },
    stopSlideShow() {
      clearInterval(this.slideShowInterval);
    },
    countWidth() {
      if (window.innerWidth < 550) {
        return false;
      } else if (window.innerWidth > 550) {
        return true;
      }
    },
    shuffleSlides() {
      let currentIndex = this.slides.length;
      let temporaryValue, randomIndex;

      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        temporaryValue = this.slides[currentIndex];
        this.slides[currentIndex] = this.slides[randomIndex];
        this.slides[randomIndex] = temporaryValue;
      }

      this.currentIndex = 0;
    },
    openFullScreen() {
      this.isFullScreen = true;
      this.stopSlideShow();
    },
    closeFullScreen() {
      this.isFullScreen = false;
      this.startSlideShow();
    },
  },
  mounted() {
    this.startSlideShow();
    this.shuffleSlides();
  },
  beforeDestroy() {
    this.stopSlideShow();
  },
};
</script>

<style scoped>
.slider {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 8px 0;
}

.slider__button {
  background-color: #8294c4;
  border: none;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 24px;
  width: 40px;
  height: 40px;
}

ion-icon {
  color: #fff;
  width: 24px;
  height: 24px;
}

.slider__button:hover {
  background-color: #acb1d6;
}

button {
  margin: 0 10px;
}

.carousel__image {
  max-width: 84%;
  background-size: cover;
  background-position: center;
  border-radius: 24px;
  transition: all 300ms ease 0s;
  cursor: pointer;
}

.fullscreen-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
  cursor: pointer;
}

.fullscreen-image {
  max-width: 90%;
  max-height: 90%;
}
</style>
