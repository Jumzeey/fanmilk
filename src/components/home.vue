<template>
  <div>
    <div class="slide-container" ref="slideContainer" :style="{ backgroundImage: containerBackground }">
      <div class="slide" v-for="(slide, index) in slides" :key="index" :data-slide-no="index + 1"
        @click="changeSlide(index)"
        :style="{ backgroundImage: `url(${slide.backgroundImage})`, top: slide.top, left: slide.left }"
        :class="{ active: currentIndex === index }"></div>

    </div>
    <!-- Description -->
    <div class="slide-description h-72 text-center text-xl text-gray-600" v-if="currentSlide"
      :style="{ bottom: currentSlide.description ? '0' : '-100px' }">
      <p class=" capitalize font-sans p-4">"{{ currentSlide.description }}""</p>
      <span class=""><button class="explore-button" v-if="currentSlide.link" @click="exploreSlide">Explore</button></span>
    </div>
    <div class="button-wrap ">
      <button type="button" class="btn btn-prev" @click="prevSlide">prev</button>
      <button type="button" class="btn btn-next" @click="nextSlide">next</button>
    </div>
  </div>
</template>

<style scoped>
* {
  padding: 0;
  margin: 0;
  border: 0;
  box-sizing: border-box;
  

}

.slide-container {
  position: relative;
  width: 35vw;
  height: 35vw;
  margin: 17vmin auto;
  border-radius: 50%;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.5);
  background-size: cover;
  background-position: center;
  transition: all 0.3s;
}

.slide {
  position: absolute;
  width: 8vw;
  height: 8vw;
  margin-top: -4vw;
  margin-left: -4vw;
  border-radius: 50%;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.3);
  background-size: cover;
  background-position: center;
  cursor: pointer;
  transform: scale(1);
  opacity: 0.9;
  transition: all 5;
}

.slide.active,
.slide:hover {
  transform: scale(1.3);
  opacity: 1;
  z-index: 100;
}

.button-wrap {
  margin-top: auto;
  display: flex;
  flex-flow: row nowrap;
}

.button-wrap .btn {
  display: block;
  flex: 1 1 auto;
  line-height: 50px;
  text-align: center;
  background: #333;
  color: #fff;
  cursor: pointer;
  text-transform: uppercase;
  font-weight: bold;
  transition: all 0.3s;
}

.button-wrap .btn:hover {
  background: #000;
}

.button-wrap .btn-prev {
  border-right: 1px solid #999;
}

.explore-button {
  display: inline-block;
  margin-top: 10px;
  padding: 8px 16px;
  background-color: #333333;
  color: white;
  border: none;
  border-radius: 25px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.explore-button:hover {
  background-color: #f6f6f6;
  color: #333333;
}

@media all and (max-width: 1024px) {
  .slide-container {
    width: 55vw;
    height: 55vw;
  }

  .slide-container .slide {
    width: 13vw;
    height: 13vw;
    margin-top: -6.5vw;
    margin-left: -6.5vw;
  }
}

@media all and (max-width: 720px) {
  .slide-container {
    width: 65vw;
    height: 65vw;
  }

  .slide-container .slide {
    width: 15vw;
    height: 15vw;
    margin-top: -7.5vw;
    margin-left: -7.5vw;
  }
}
</style>

<script>
export default {
  data() {
    return {
      slides: [
        {
          backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/choco_CEtlXVfZO.jpeg?updatedAt=1691766414371',
          top: '',
          left: '',
          description: 'Fanchoco is a chocolate flavoured frozen milk drink. It has the goodness and benefits of cocoa and contains vitamin & minerals such as B2, B6, thiamine, calcium & phosphorus.',
          link: 'https://example.com/slide1'
        },
        {
          backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/citrus_eREM96NYQ.jpeg?updatedAt=1691766454371',
          top: '',
          left: '',
          link: 'https://example.com/slide1',
          description: 'Fandango is a refreshing citrus fruit drink that is enriched with Vitamin C and is available in both frozen(sachet) and ambient (PET bottle) formats.'
        },
        {
          backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/apple_1N0ea5jgq.jpeg?updatedAt=1691766499778',
          top: '',
          left: '',
          link: 'https://instagram.com/superyogong?igshid=MzRlODBiNWFlZA==',
          description: 'Superyogo is a fortified sweetened frozen yoghurt snack packed with essential nutrients like Vitamin B2, B6,calcium, iodine and phosphorous.'
        },
        {
          backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/strawberry_Px0h7GUft.jpeg?updatedAt=1691766550979',
          top: '',
          left: '',
          link: 'https://example.com/slide1',
          description: 'FanMilk flavoured creamy drink is anaffordable refreshing flavoured milkdrink that is available in coolflavours such as strawberry,apple, orange, pineapple, mango in frozen (sachet) format.'
        },
        {
          backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/vanilla_hTZDUE1Jh.jpeg?updatedAt=1691766597686',
          top: '',
          left: '',
          link: 'https://instagram.com/fanvanilleng?igshid=MzRlODBiNWFlZA==',
          description: 'Fanvanille is a frozen flavoured milk drink that combines milk & vanilla to create a unique taste that has fast become the number 1 frozen dairy milk brand in Nigeria.'
        },
        // ... add other slide URLs
      ],
      currentIndex: 0,
      angle: 360 / 5, // Assuming there are 12 slides
      setId: null,
      currentSlide: null,
    };
  },
  computed: {
    containerBackground() {
      return `url(${this.slides[this.currentIndex].backgroundImage})`;
    },
    currentSlide() {
      return this.slides[this.currentIndex];
    },
  },
  methods: {
    positionSlides() {
      const container = this.$refs.slideContainer;
      const r = container.offsetWidth / 2;

      for (let i = 0; i < this.slides.length; i++) {
        const deg = i * this.angle;
        const x = Math.cos(deg * (Math.PI / 180)) * r + r;
        const y = Math.sin(deg * (Math.PI / 180)) * r + r;
        // this.slides[i].top = Math.floor(y) + 'px';
        // this.slides[i].left = Math.floor(x) + 'px';
      }
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + this.slides.length) % this.slides.length;
      this.animateSlide();
    },
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.slides.length;
      this.animateSlide();
    },
    animateSlide() {
      const r = this.$refs.slideContainer.offsetWidth / 2;
      for (let i = 0; i < this.slides.length; i++) {
        const deg = (i * this.angle + 360 * this.currentIndex) % 360;
        const x = Math.cos(deg * (Math.PI / 180)) * r + r;
        const y = Math.sin(deg * (Math.PI / 180)) * r + r;
        this.slides[i].top = Math.floor(y) + 'px';
        this.slides[i].left = Math.floor(x) + 'px';
      }
    },
    exploreSlide() {
      const currentSlide = this.slides[this.currentIndex];
      if (currentSlide.link) {
        window.open(currentSlide.link, '_blank');
      }
    },
    changeSlide(index) {
      this.currentIndex = index;
      this.animateSlide();
    },
    autoPlay() {
      this.setId = setInterval(this.nextSlide, 3000);
    },
    pauseAutoPlay() {
      clearInterval(this.setId);
    },

    resumeAutoPlay() {
      clearInterval(this.setId);
      this.autoPlay();
    },
  },
  mounted() {
    this.positionSlides();
    this.animateSlide();
    this.autoPlay();

    // Pause autoplay on slide hover
    this.$refs.slideContainer.addEventListener('mouseenter', this.pauseAutoPlay);

    // Resume autoplay on slide hover out
    this.$refs.slideContainer.addEventListener('mouseleave', this.resumeAutoPlay);

    // Pause autoplay when previous or next button is pressed
    this.$refs.btnPrev.addEventListener('click', this.pauseAutoPlay);
    this.$refs.btnNext.addEventListener('click', this.pauseAutoPlay);
  },
};
</script>
