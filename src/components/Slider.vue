<template>
  <div class="wrapper">
    <SliderItem v-for="slide in slides" :key="slide.id">
      <div class="slider__wrapper" :style="getTransform(slide)">
        <div id="button" @click="nextSlide(slide.id)">
          <img src="../assets/images/text.svg" alt="Kiwi standing on oval" />
          <span>&#8594;</span>
        </div>
        <img id="star" src="../assets/images/star.png" alt="Dog" />

        <div class="slider__content">
          <p class="slider__caption">Lorem ipsum dolor sit amet</p>
          <h1 class="slider__header">lorem ipsum</h1>
          <p class="slider__title">
            Lorem ipsum dolor — <br />
            <span class="line-one">Lorem</span><br /><span class="line-two"
              >ipsum !</span
            >
          </p>
          <p class="slider__note">
            Lorem ipsum dolor sit amet,<br />consectetur adipiscing elit
          </p>
        </div>
        <div class="slider__ovals">
          <div id="oval-one" class="slider__oval"></div>
          <div id="oval-two" class="slider__oval"></div>
          <div id="oval-three" class="slider__oval"></div>
          <div id="oval-four" class="slider__oval">
            <img src="../assets/images/dog.jpg" alt="Dog" />
          </div>
          <!-- <button >CLICK ME</button> -->
        </div>
        <div id="oval-five" class="slider__oval">
          <p>{{ currentSlide }} / {{ slides.length }}</p>
        </div>
      </div>
    </SliderItem>
  </div>
</template>

<script>
import SliderItem from "./SliderItem.vue";
export default {
  components: {
    SliderItem,
  },
  data() {
    return {
      currentSlide: 1,
    };
  },
  props: {
    slides: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    nextSlide(index) {
      const temp = this.slides[index];
      temp.id = this.slides.length - 1;
      this.slides.splice(index, 1);

      //  temp.id +=1;
      this.slides.forEach((element) => {
        element.id -= 1;
      });

      // console.log("temp",temp)
      this.slides.push(temp);
      console.log(this.slides);
      this.currentSlide += 1;
      if (this.currentSlide == this.slides.length + 1) {
        this.currentSlide = 1;
      }
    },
    getTransform(item) {
      return {
        transform: `translateX(${item.id * 64}px)`,
        backgroundColor: `${item.color}`,
        zIndex: `${item.id * -1}`,
      };
    },
  },
};
</script>

<style lang="scss" scoped>
/* различные продолжительности и динамику.       */
.wrapper {
  max-width: 100%;
height: 628px;
  overflow: hidden;
  position: relative;
}
.slider {
  &__wrapper {
    position: absolute;
    top: 0;
    left: 0;
    height: 602px;
    max-height: 700px;
    // min-width: 1024px;
    min-width: 20%;
    max-width: 100%;
    width: 91%;
    border-top-right-radius: 35px;
    border-bottom-right-radius: 35px;
    color: #fff;
    text-transform: uppercase;
    display: flex;
    flex-direction: row;
    transition: all 1s ease-in-out;
  }
  &__content {
    position: relative;

    width: 80%;
  }
  &__ovals {
    position: relative;
    width: 20%;
  }
  &__oval {
    position: absolute;
    width: 465px;
    height: 250px;
    background: #afb3b4;
    border-radius: 50%;
    z-index: -1;
  }
  &__caption {
    font-size: 17px;
    /* text-align: center; */
    color: #fff;
    padding: 14px 0 0px 159px;
    text-shadow: 4px 4px 4px rgba(0, 0, 0, 0.25);
  }
  &__header {
    font-size: 52px;
    padding: 60px 0 0 129px;
  }
  &__title {
    font-size: 51px;
    padding: 0px 0 0 164px;
    & .line-one {
      display: inline-block;
      padding: 0 0 0 210px;
    }
    & .line-two {
      display: inline-block;
      padding: 0 0 0 84px;
    }
  }
  &__note {
    font-size: 13px;
    padding: 33px 0 0 369px;
    line-height: 19px;
  }
}
#button {
  /* width: 100%; */
  /* height: 200px; */
  /* display: block; */
  position: absolute;
  width: 130px;
  height: 130px;
  z-index: 1;
  top: 240px;
  left: 84%;
  cursor: pointer;
  span {
    position: absolute;
    top: 45%;
    left: 50%;
    transform: translate(-50%, -45%);
    font-size: 40px;
    color: white;
  }
}
#oval-one {
  top: -205px;
  left: -952px;
  transform: rotate(21.28deg);
}
#oval-two {
  top: 280px;
  left: -290px;
  transform: rotate(164.28deg);
  width: 393px;
  height: 200px;
}
#oval-three {
  top: 141px;
  left: -265px;
  transform: rotate(220.28deg);
  width: 395px;
  height: 205px;
  background: transparent;
  border: 2px solid #fff;
}
#oval-four {
  top: 283px;
  left: -379px;

  transform: rotate(140.28deg);
  width: 394px;
  height: 205px;
  background: transparent;
  overflow: hidden;
  img {
    position: absolute;
    transform: rotate(221deg);
    top: -80px;
    left: 7px;
  }
}
#star {
  position: absolute;
  top: 290px;
  left: -11px;
}
#oval-five {
  top: 504px;
  left: 202px;
  width: 94px;
  height: 50px;
  background: transparent;
  border: 2px solid #fff;
  p {
    font-size: 14px;
    padding: 16px 0;
    text-align: center;
  }
}
@media screen and (min-width: 1440px) {
  #oval-one {
    left: -1044px;
  }
}
@media (min-width: 1024px) and (max-width: 1025px) {
  .slider {
    &__wrapper {
      //          min-width: 88%;
      // width: 91%;
      width: 87.5%;
    }
    &__header {
      font-size: 31px;
    }
    &__caption {
      font-size: 20px;
    }
    &__title {
      font-size: 41px;
      & .line-one {
        padding: 0 0 0 170px;
      }
    }
    &__note {
      padding: 143px 0 0 159px;
    }
    #oval-five {
      top: 524px;
      left: 42px;
    }
    #oval-one {
      left: -502px;
    }
  }
}
@media (max-width: 768px) {
  .slider {
    &__wrapper {
      //          min-width: 88%;
      // width: 91%;
      width: 83.2%;
    }
    &__header {
      font-size: 31px;
      padding-left: 19px;
    }
    &__caption {
      font-size: 16px;
    }
    &__title {
      font-size: 31px;
      padding-left: 34px;
      & .line-one {
        padding: 0 0 0 170px;
      }
    }
    &__note {
    padding: 3px 0 0 249px
    }
    &__ovals{
     
    #oval-one {
      left: -502px;
    }
    }
    
  }
     #oval-five {
   top: 534px;
    left: 22px;
    }
    #oval-two{
    width: 323px;
    top: 410px;
    left: -350px;
    height: 150px;
    }
    #oval-three{
            width: 275px;
    height: 155px;
top: 321px;
    left: -286px;
    }
    #oval-four{
        width: 314px;
    height: 175px;

    top: 353px;
    left: -399px;

    }
  #button{
        left: 71%;
    }
    #star{
        top: 180px;
    left: -61px;
    }
}
</style>