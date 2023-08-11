<!-- <template>
  <div class="flex-center">
    <div class="circular-slider">
      <ul class="wrapper flex-center">
        <li class="slides" v-for="image in images "
          :style="{ 'transform': `rotateZ(${calculateRotation(image.imgNo)}deg) translateY(25rem)` }"
          @mouseover="scaleImageUp(image.imgNo)"
          @mouseout="resetImageScale(image.imgNo)"
          >
          <img 
          :src="image.src" alt="" 
          :style="{
              'transform': `rotateZ(${calculateRotationimg(image.imgNo)}deg) scale(${image.scale})`,
              'transition': 'transform 0.3s ease-in-out'
            }"
          
          >
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      images: [
        { src: 'https://ik.imagekit.io/jumzeey/fanmilk/WhatsApp%20Image%202023-08-10%20at%207.27.39%20PM%20(2)_OuShNWMW9.jpeg?updatedAt=1691745772708', imgNo: 1, scale:1 },
        { src: 'https://ik.imagekit.io/jumzeey/fanmilk/WhatsApp%20Image%202023-08-10%20at%207.27.39%20PM%20(3)_5uSeZ4N5T.jpeg?updatedAt=1691745769442', imgNo: 2, scale:1  },
        { src: 'https://ik.imagekit.io/jumzeey/fanmilk/WhatsApp%20Image%202023-08-10%20at%207.27.39%20PM%20(1)_6_SFDAnrt.jpeg?updatedAt=1691745769423', imgNo: 3, scale:1  },
        { src: 'https://ik.imagekit.io/jumzeey/fanmilk/WhatsApp%20Image%202023-08-10%20at%207.27.39%20PM_LH7RQNaz9.jpeg?updatedAt=1691745769384', imgNo: 4, scale:1  },
      ],

    }
  },
  methods: {
    calculateRotation(imgNo) {
      // Calculate the rotation angle based on imgNo
      const numImages = 5;
      const angle = (360 / numImages) * imgNo;
      return angle;
    },
    calculateRotationimg(imgNo) {
      // Calculate the rotation angle based on imgNo
      const numImages = -5;
      const angle = (360 / numImages) * imgNo;
      return angle;
    },
    scaleImageUp(imgNo) {
      const image = this.images.find(img => img.imgNo === imgNo);
      if (image) {
        image.scale = 1.2; // Increase scale on hover
      }
    },
    resetImageScale(imgNo) {
      const image = this.images.find(img => img.imgNo === imgNo);
      if (image) {
        image.scale = 1; // Reset scale on hover out
      }
    }
  }
}
</script>

Add "scoped" attribute to limit CSS to this component only
<style scoped>
/* Use CSS variables here */
.circular-slider {
  height: var(--slider-height);
  /* Using the defined variable */
}

/* Rest of your styles */
:root {
  --dark-blue: #04021f;
  --sky-blue: #00abf1;
  --slider-height: 50rem;
  --half-slider-height: calc(var(--slider-height) / 2);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style-type: none;
  border: none;
  font-family: sans-serif;
}

body {
  min-height: 100vh;
  background-color: #04021f;
}

.flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.slides {
  width: 20vw;
  position: absolute;
  transform-origin: 25rem;
  left: 0;
  cursor: pointer;
}

.slides img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
}

.circular-slider {
  position: relative;
  top:12vh;
  width: 50rem;
  height: 50rem;
  color: #fff;
  text-align: center;
}

.wrapper {
  position: absolute;
  width: 100%;
  height: 100%;
  border: 1px solid crimson;
  border-radius: 50%;
  transform: rotateZ(0deg);
  transition: 1s ease-in-out;
}
.slides img:hover {
  transform: scale(1.2); /* Scale the image on hover */
}

/* Positioning for different images */
.slides:nth-child(1) {
  transform: translateY(-25rem) rotateZ(0deg);
}

.slides:nth-child(2) {
  transform: translateY(25rem) rotateZ(180deg);
}

.slides:nth-child(3) {
  transform: translateX(-25rem) rotateZ(90deg);
}

.slides:nth-child(4) {
  transform: translateX(25rem) rotateZ(-90deg);
}
</style> -->
<template>
  <div class="slide-container" ref="slideContainer" :style="{ backgroundImage: containerBackground }">
    <div
      class="slide"
      v-for="(slide, index) in slides"
      :key="index"
      :data-slide-no="index + 1"
      @click="changeSlide(index)"
      :style="{ backgroundImage: `url(${slide.backgroundImage})`, top: slide.top, left: slide.left }"
      :class="{ active: currentIndex === index }"
    ></div>
  </div>
  <div class="button-wrap">
    <button type="button" class="btn btn-prev" @click="prevSlide">prev</button>
    <button type="button" class="btn btn-next" @click="nextSlide">next</button>
  </div>
</template>

<style scoped>
* {
  padding: 0;
  margin: 0;
  border: 0;
  box-sizing: border-box;
  background-color: #fec89a;
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
  transition: all 0.3s;
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
        { backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/choco_CEtlXVfZO.jpeg?updatedAt=1691766414371', top: '', left: '' },
        { backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/citrus_eREM96NYQ.jpeg?updatedAt=1691766454371', top: '', left: '' },
        { backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/apple_1N0ea5jgq.jpeg?updatedAt=1691766499778', top: '', left: '' },
        { backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/strawberry_Px0h7GUft.jpeg?updatedAt=1691766550979', top: '', left: '' },
        { backgroundImage: 'https://ik.imagekit.io/jumzeey/fanmilk/vanilla_hTZDUE1Jh.jpeg?updatedAt=1691766597686', top: '', left: '' },
        // ... add other slide URLs
      ],
      currentIndex: 0,
      angle: 360 / 5, // Assuming there are 12 slides
      setId: null,
    };
  },
  computed: {
    containerBackground() {
      return `url(${this.slides[this.currentIndex].backgroundImage})`;
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
    changeSlide(index) {
      this.currentIndex = index;
      this.animateSlide();
    },
    autoPlay() {
      this.setId = setInterval(this.nextSlide, 3000);
    },
  },
  mounted() {
    this.positionSlides();
    this.animateSlide();
    this.autoPlay();
  },
};
</script>
