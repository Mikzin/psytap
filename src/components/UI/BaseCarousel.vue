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
      @touchstart="handleTouchStart"
      @touchend="handleTouchEnd"
    />
    <button v-if="!isMobile" class="arrow left-arrow" @click="prevSlide">
      ‹
    </button>
    <button v-if="!isMobile" class="arrow right-arrow" @click="nextSlide">
      ›
    </button>
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
      touchStartX: 0,
      isMobile: window.innerWidth <= 767,
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
          this.nextSlide();
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
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
    },
    prevSlide() {
      this.currentIndex =
        (this.currentIndex - 1 + this.slides.length) % this.slides.length;
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
    handleTouchStart(event) {
      this.touchStartX = event.changedTouches[0].screenX;
    },
    handleTouchEnd(event) {
      const touchEndX = event.changedTouches[0].screenX;
      if (this.touchStartX - touchEndX > 50) {
        this.nextSlide();
      } else if (this.touchStartX - touchEndX < -50) {
        this.prevSlide();
      }
    },
  },
  mounted() {
    this.preloadImages();
    this.startSlideShow();
    window.addEventListener('resize', () => {
      this.isMobile = window.innerWidth <= 767;
    });
  },
  beforeDestroy() {
    this.stopSlideShow();
    window.removeEventListener('resize', () => {
      this.isMobile = window.innerWidth <= 767;
    });
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

.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 24px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
}

.left-arrow {
  left: 10px;
}

.right-arrow {
  right: 10px;
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

  .carousel__image {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }
}
</style>
