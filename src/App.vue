<template>
  <section class="slider">
    <article class="slider__slide parallax">
      <transition-group name="slider__content" mode="out-in">
        <figure
          v-for="item in slides"
          :key="item.id"
          class="slider__content"
          :style="{
            backgroundImage: 'url(' + item.image + ')',
            opacity: currentSlide === item.id ? '1' : '0'
          }"
        >
          <figcaption class="slider__caption">
            <span class="slider__textFix">
              <h2 class="slider__header">{{ item.title }}</h2>
              <p class="slider__title">{{ item.description }}</p>
            </span>
          </figcaption>
        </figure>
      </transition-group>
    </article>
    <p class="tester"></p>
  </section>
</template>

<script>
export default {
  name: "slider",
  data() {
    return {
      timer: "",
      currentSlide: 0,
      slides: [
        {
          id: 0,
          title: "#SVAGPL",
          description: "Mikołajkowy Zlot",
          image: "./img/seat1.jpg",
          altDesc: "#svagpl"
        },
        {
          id: 1,
          title: "#Cars Team Działdowo",
          description: "Zakończenie sezonu",
          image: "./img/seat2.jpg",
          altDesc: "#carsteamdzialdowo"
        },
        {
          id: 2,
          title: "#WPZ Audi",
          description: "Bunt i stracone dowody",
          image: "./img/seat3.jpg",
          altDesc: "#wpzaudi"
        },
        {
          id: 3,
          title: "#MNR",
          description: "Gdzie się podziali?",
          image: "./img/seat4.jpg",
          altDesc: "mnr"
        },
        {
          id: 4,
          title: "#Maniek",
          description: "Szybszy niż wszyscy",
          image: "./img/seat5.jpg",
          altDesc: "#maniek"
        }
      ]
    };
  },
  watch: {
    timer() {
      console.log(this);
    }
  },
  methods: {
    changeSlide() {
      this.currentSlide = Math.floor(Math.random() * this.slides.length);
    }
  },
  created() {
    this.timer = setInterval(this.changeSlide, 10000);
  },
  beforeDestroy() {
    clearInterval(this.timer);
  }
};
</script>

<style lang="scss">
$colorMain: #990000;
// font-family: 'Noto Sans', sans-serif;
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans:ital,wght@0,400;0,700;1,400;1,700&display=swap");
// @import url('');
$tablet: "(min-width: 640px) and (max-width: 1023px)";
$desktop: "(min-width: 1024px)";

* {
  box-sizing: border-box;
  font-family: inherit;
  list-style-type: inherit;
  text-decoration: inherit;
  color: inherit;
  cursor: pointer;
  margin: 0;
  padding: 0;
  width: 100%;
}

.tester {
  height: 1000px;
  background-color: black;
}

.slider {
  height: 25vh;
  width: 100%;
  background-color: black;
  font-family: "Noto Sans", sans-serif;
  text-align: left;
  text-transform: lowercase;
  position: relative;
  &__slide {
    width: 100%;
    height: 100%;
  }
  &__content {
    width: 100%;
    height: 100%;
    background-size: 100% 100%;
    background-attachment: fixed;
    opacity: 1;
    transition: 0.5s ease-in-out;
    position: absolute;
    top: 0;
    &-enter-active,
    &-leave-active {
      transition: opacity 0.3s ease;
    }
    &-enter {
      opacity: 0;
    }
    &-leave-to {
      opacity: 0;
    }
  }
  &__image {
    width: 100%;
    height: 100%;
    // position: fixed;
  }
  &__caption {
    width: 100%;
    height: 12vh;
    position: absolute;
    bottom: 0;
  }
  &__header {
    color: #fff;
    font-size: 30px;
    text-shadow: #000 1px 1px;
  }
  &__title {
    color: $colorMain;
    font-weight: bold;
    font-size: 15px;
    text-shadow: #fff 1px 1px, #fff -1px -1px, #fff -1px 1px, #fff 1px -1px;
  }
  &__textFix {
    width: auto;
    position: absolute;
    right: 10vw;
  }
}

@media #{$tablet} {
  .slider {
    height: 80vh;
    &__header {
      font-size: 25px;
    }
    &__title {
      font-size: 20px;
    }
    &__caption {
      height: 15vh;
      bottom: 16vh;
    }
    &__textFix {
      right: 10vw;
    }
  }
}
@media #{$desktop} {
  .slider {
    height: 100vh;
    &__header {
      font-size: 40px;
    }
    &__title {
      font-size: 25px;
    }
    &__caption {
      height: 15vh;
      bottom: 16vh;
    }
    &__textFix {
      right: 10vw;
    }
  }
}
</style>
