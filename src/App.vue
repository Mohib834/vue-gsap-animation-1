<template>
  <div id="app">
    <div class="container">
      <nav>
        <h3>Logo</h3>
        <ul>
          <li>About us</li>
          <li>/</li>
          <li>
            <strong>Menu</strong>
          </li>
          <li @click="animate">Start</li>
        </ul>
      </nav>
      <main ref="main">
        <div class="main-content">
          <h1 class="main-content-heading" ref="title">About us</h1>
          <div class="main-content-images">
            <img ref="img" width="200" v-for="(img, i) in imgs" :key="i" :src="img.src" />
          </div>
          <a href="#" @click.prevent="enterAnimate" ref="enterBtn" class="enter-btn">Enter &rarr;</a>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import { gsap, Back } from "gsap";
import img1 from "./assets/1.jpg";
import img2 from "./assets/2.jpg";
import img3 from "./assets/3.jpg";
import img4 from "./assets/4.jpg";

export default {
  data() {
    return {
      imgs: [{ src: img1 }, { src: img2 }, { src: img3 }, { src: img4 }]
    };
  },
  mounted() {},
  methods: {
    animate() {
      const imgs = this.$refs.img;
      const main = this.$refs.main;
      const aboutTitle = this.$refs.title;
      const enterBtn = this.$refs.enterBtn;

      const tl = gsap.timeline();

      tl.from(aboutTitle, 1, { y: 400, ease: Back.easeOut.config(1) })
        .to(main, { visibility: "visible" })
        .from(
          imgs,
          1.6,
          {
            y: 1000,
            stagger: 0.15,
            ease: Back.easeOut.config(0.5)
          },
          "-=1"
        )
        .from(
          enterBtn,
          0.5,
          {
            opacity: 0
          },
          "-=1"
        );
    },
    enterAnimate() {
      const imgs = this.$refs.img;
      const aboutTitle = this.$refs.title;
      const enterBtn = this.$refs.enterBtn;

      const tl = gsap.timeline();

      tl.to(imgs, 1.5, { scale: 0.01, opacity: 0, left: 20, top: -200 })
        .to(aboutTitle, 1.5, { scale: 0.01, opacity: 0 }, "-=1.5")
        .to(enterBtn, 0.5, { opacity: 0 }, "-=1.5");
    }
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
#app {
  height: 100vh;
  background: #eee;
  font-family: "Roboto", sans-serif;
  letter-spacing: 1.1px;
  overflow: hidden;
}

.container {
  width: 1260px;
  margin: auto;
  height: 100%;
}

nav {
  padding: 2rem 0;
  display: flex;
  justify-content: space-between;
}

nav ul {
  list-style: none;
  display: flex;
  font-size: 14px;
}

nav ul li {
  margin-right: 10px;
}

nav ul li:nth-of-type(2) {
  margin-left: 20px;
  margin-right: 20px;
}

main {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 86vh;
  position: relative;
  visibility: hidden;
}

.main-content-heading {
  font-size: 85px;
  letter-spacing: 2px;
  color: #fff;
  top: -40px;
  position: relative;
  z-index: 100;
  text-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.main-content-images {
  position: relative;
}

.main-content-images img {
  position: absolute;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.main-content-images img:nth-of-type(1) {
  top: -20px;
  left: -157px;
  width: 332px;
  z-index: 10;
}

.main-content-images img:nth-of-type(2) {
  top: -333px;
  left: 70px;
  width: 265px;
}
.main-content-images img:nth-of-type(3) {
  bottom: -45px;
  right: -214px;
  width: 250px;
}
.main-content-images img:nth-of-type(4) {
  top: -200px;
  left: -200px;
  width: 350px;
}

.main-content {
  position: relative;
}

.main-content .enter-btn {
  position: absolute;
  right: 26px;
  bottom: -104px;
  color: #333;
  text-decoration: none;
}

.main-content .enter-btn::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  border-bottom: 1px solid #333;
  transition: all 0.3s ease-out;
  width: 0;
}

.main-content .enter-btn:hover::after {
  width: 100%;
}
</style>
 