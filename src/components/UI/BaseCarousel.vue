<template>
  <div class="slider">
    <img
      v-for="(slide, index) in preloadedImages"
      :key="index"
      :src="slide"
      alt="Slide"
      class="carousel__image"
      :class="{ active: index === currentIndex }"
      @mouseenter="stopSlideShow"
      @mouseleave="startSlideShow"
      @click="openFullScreen"
    />
  </div>

  <div class="pagination">
    <button
      v-for="(slide, index) in slides"
      :key="index"
      @click="goToSlide(index)"
      :class="[
        'pagination__button',
        { 'pagination__button--active': index === currentIndex },
      ]"
    ></button>
  </div>

  <div class="fullscreen__overlay" v-if="isFullScreen" @click="closeFullScreen">
    <img :src="currentSlide" alt="Slide" class="fullscreen__image" />
  </div>
</template>

<script>
import image1 from '../../images/1.jpg';
import image2 from '../../images/2.jpg';
import image3 from '../../images/3.jpg';

export default {
  data() {
    return {
      slides: [image1, image2, image3],
      currentIndex: 0,
      isHovered: false,
      isFullScreen: false,
      preloadedImages: [],
    };
  },
  computed: {
    currentSlide() {
      return (
        this.preloadedImages[this.currentIndex] ||
        this.slides[this.currentIndex]
      );
    },
  },
  methods: {
    startSlideShow() {
      if (!this.isHovered && !this.isFullScreen) {
        this.slideShowInterval = setInterval(() => {
          this.currentIndex = (this.currentIndex + 1) % this.slides.length;
        }, 3000);
      }
    },
    stopSlideShow() {
      clearInterval(this.slideShowInterval);
    },
    openFullScreen() {
      this.isFullScreen = true;
      this.stopSlideShow();
    },
    closeFullScreen() {
      this.isFullScreen = false;
      this.startSlideShow();
    },
    goToSlide(index) {
      this.currentIndex = index;
      this.stopSlideShow();
      this.startSlideShow();
    },
    preloadImages() {
      this.slides.forEach((slide, index) => {
        const img = new Image();
        img.src = slide;
        img.onload = () => {
          console.log(`Image ${index + 1} loaded`);
          this.preloadedImages[index] = img.src;
        };
        img.onerror = (error) => {
          console.error(`Failed to load image ${index + 1}:`, error);
        };
      });
    },
  },
  mounted() {
    this.preloadImages();
    this.startSlideShow();
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
  position: relative;
  width: 100%;
  max-width: 700px;
  height: 400px;
  overflow: hidden;
}

.carousel__image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  border-radius: 24px;
  transition: all 300ms ease 0s;
  cursor: pointer;
  display: none;
}

.carousel__image.active {
  display: block;
}

.pagination {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.pagination__button {
  width: 12px;
  height: 12px;
  background-color: #c4c4c4;
  border: none;
  border-radius: 50%;
  margin: 0 5px;
  cursor: pointer;
  flex-shrink: 0;
  transition: background-color 0.3s ease;
}

.pagination__button--active {
  background-color: #8294c4;
}

.fullscreen__overlay {
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

.fullscreen__image {
  max-width: 90%;
  max-height: 90%;
  object-fit: contain;
}

@media (max-width: 767px) {
  .slider {
    width: 100%;
    height: 400px;
    max-height: 400px;
  }

  .pagination__button {
    width: 12px;
    height: 12px;
  }

  .carousel__image {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }
}

@media (max-width: 480px) {
  .pagination__button {
    width: 10px;
    height: 10px;
  }
}
</style>
