<template>
  <div>
    <div class="clock-container">
    <div class="clock animate__heartBeat">
      <div class="current-time" style="margin-top: -35px;">
        <div v-if="stopped" class="animate__animated animate__backInUp">
          {{ getCurrentTime() }}
        </div>
      </div>
      <div class="clock-face">
        <div v-if="!stopped">
          <div class="second-hand hand1"></div>
          <div class="second-hand hand2"></div>
        </div>
        <div v-else>
          <div class="second-hand" :style="{ transform: secondHandTransform }"></div>
          <div class="minute-hand" :style="{ transform: minuteHandTransform }"></div>
          <div class="hour-hand" :style="{ transform: hourHandTransform }"></div>
        </div>
      </div>
    </div>
  </div>
    <!-- <div class="section full-height">
      <div class="absolute-center">
        <div class="section">
          <div class="container">
            <div class="row">
              <div class="col-12">
                <h1>
                  <span>B</span><span>o</span><span>o</span><span>t</span
                  ><span>s</span><span>t</span><span>r</span><span>a</span
                  ><span>p</span> <span>4</span><br />
                  <span>m</span><span>e</span><span>n</span><span>u</span>
                </h1>
              </div>
            </div>
          </div>
        </div>
        <div class="section mt-5">
          <div class="container">
            <div class="row">
              <div class="col-12">
                <div id="switch">
                  <div id="circle"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div> -->
    <div class="my-5 py-5"></div>
    <a href="http://localhost:8080/" class="logo" target="_blank">
      <img src="@/assets/jk.png" alt="" />
    </a>
  </div>
</template>

<script>
export default {
  data() {
    return {
      headerClass: "start-style",
      isDarkMode: false,
      stopped: false,
      secondHandTransform: "",
      minuteHandTransform: "",
      hourHandTransform: "",
    };
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
    this.animateHero()
    this.updateClockHands();
    setInterval(this.updateClockHands, 100);
    setTimeout(() => {
      this.stopClock();
    }, 5000);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      const scroll = window.scrollY;
      if (scroll >= 10) {
        this.headerClass = "scroll-on";
      } else {
        this.headerClass = "start-style";
      }
    },
    animateHero() {
      this.$nextTick(() => {
        this.$el.classList.remove("hero-anime");
      });
    },
    toggleDarkMode() {
      this.isDarkMode = !this.isDarkMode;
    },
    updateClockHands() {
      const date = new Date();
      const seconds = date.getSeconds();
      const minutes = date.getMinutes();
      const hours = date.getHours();

      const secondHandAngle = (seconds / 60) * 360;
      this.secondHandTransform = `rotate(${secondHandAngle}deg)`;

      const minuteHandAngle = (minutes / 60) * 360 + (seconds / 60) * 6;
      this.minuteHandTransform = `rotate(${minuteHandAngle}deg)`;

      const hourHandAngle = (hours / 12) * 360 + (minutes / 60) * 30;
      this.hourHandTransform = `rotate(${hourHandAngle}deg)`;
    },

    stopClock() {
      this.stopped = true;
    },

    getCurrentTime() {
      const date = new Date();
      const hours = date.getHours();
      const minutes = date.getMinutes();
      const seconds = date.getSeconds();

      return `${this.addLeadingZero(hours)}:${this.addLeadingZero(
        minutes
      )}:${this.addLeadingZero(seconds)}`;
    },

    addLeadingZero(value) {
      return value < 10 ? `0${value}` : value;
    },
  },
};
</script>

<style lang="scss">
/* Please ❤ this if you like it! */

@import url("https://fonts.googleapis.com/css?family=Poppins:100,100i,200,200i,300,300i,400,400i,500,500i,600,600i,700,700i,800,800i,900,900i&subset=devanagari,latin-ext");

/* #Primary
================================================== */

body {
  font-family: "Poppins", sans-serif;
  font-size: 16px;
  line-height: 24px;
  font-weight: 400;
  color: #212112;
  background-image: url("https://s3-us-west-2.amazonaws.com/s.cdpn.io/1462889/pat-back.svg");
  background-position: center;
  background-repeat: repeat;
  background-size: 7%;
  background-color: #fff;
  overflow-x: hidden;
  transition: all 200ms linear;
}
::selection {
  color: #fff;
  background-color: #8167a9;
}
::-moz-selection {
  color: #fff;
  background-color: #8167a9;
}

/* #Navigation
================================================== */

.start-header {
  opacity: 1;
  transform: translateY(0);
  padding: 20px 0;
  box-shadow: 0 10px 30px 0 rgba(138, 155, 165, 0.15);
  -webkit-transition: all 0.3s ease-out;
  transition: all 0.3s ease-out;
}
.start-header.scroll-on {
  box-shadow: 0 5px 10px 0 rgba(138, 155, 165, 0.15);
  padding: 10px 0;
  -webkit-transition: all 0.3s ease-out;
  transition: all 0.3s ease-out;
}
.start-header.scroll-on .navbar-brand img {
  height: 24px;
  -webkit-transition: all 0.3s ease-out;
  transition: all 0.3s ease-out;
}
.navigation-wrap {
  position: fixed;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 1000;
  -webkit-transition: all 0.3s ease-out;
  transition: all 0.3s ease-out;
}
.navbar {
  padding: 0;
}
.navbar-brand img {
  height: 28px;
  width: auto;
  display: block;
  filter: brightness(10%);
  -webkit-transition: all 0.3s ease-out;
  transition: all 0.3s ease-out;
}
.navbar-toggler {
  float: right;
  border: none;
  padding-right: 0;
}
.navbar-toggler:active,
.navbar-toggler:focus {
  outline: none;
}
.navbar-light .navbar-toggler-icon {
  width: 24px;
  height: 17px;
  background-image: none;
  position: relative;
  border-bottom: 1px solid #000;
  transition: all 300ms linear;
}
.navbar-light .navbar-toggler-icon:after,
.navbar-light .navbar-toggler-icon:before {
  width: 24px;
  position: absolute;
  height: 1px;
  background-color: #000;
  top: 0;
  left: 0;
  content: "";
  z-index: 2;
  transition: all 300ms linear;
}
.navbar-light .navbar-toggler-icon:after {
  top: 8px;
}
.navbar-toggler[aria-expanded="true"] .navbar-toggler-icon:after {
  transform: rotate(45deg);
}
.navbar-toggler[aria-expanded="true"] .navbar-toggler-icon:before {
  transform: translateY(8px) rotate(-45deg);
}
.navbar-toggler[aria-expanded="true"] .navbar-toggler-icon {
  border-color: transparent;
}
.nav-link {
  color: #212121 !important;
  font-weight: 500;
  transition: all 200ms linear;
}
.nav-item:hover .nav-link {
  color: #8167a9 !important;
}
.nav-item.active .nav-link {
  color: #777 !important;
}
.nav-link {
  position: relative;
  padding: 5px 0 !important;
  display: inline-block;
}
.nav-item:after {
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 100%;
  height: 2px;
  content: "";
  background-color: #8167a9;
  opacity: 0;
  transition: all 200ms linear;
}
.nav-item:hover:after {
  bottom: 0;
  opacity: 1;
}
.nav-item.active:hover:after {
  opacity: 0;
}
.nav-item {
  position: relative;
  transition: all 200ms linear;
}

/* #Primary style
================================================== */

.bg-light {
  background-color: #fff !important;
  transition: all 200ms linear;
}
.section {
  position: relative;
  width: 100%;
  display: block;
}
.full-height {
  height: 100vh;
}
.over-hide {
  overflow: hidden;
}
.absolute-center {
  position: absolute;
  top: 50%;
  left: 0;
  width: 100%;
  margin-top: 40px;
  transform: translateY(-50%);
  z-index: 20;
}
h1 {
  font-size: 48px;
  line-height: 1.2;
  font-weight: 700;
  color: #212112;
  text-align: center;
}
p {
  text-align: center;
  margin: 0;
  padding-top: 10px;
  opacity: 1;
  transform: translate(0);
  transition: all 300ms linear;
  transition-delay: 1700ms;
}
body.hero-anime p {
  opacity: 0;
  transform: translateY(40px);
  transition-delay: 1700ms;
}
h1 span {
  display: inline-block;
  transition: all 300ms linear;
  opacity: 1;
  transform: translate(0);
}
body.hero-anime h1 span:nth-child(1) {
  opacity: 0;
  transform: translateY(-20px);
}
body.hero-anime h1 span:nth-child(2) {
  opacity: 0;
  transform: translateY(-30px);
}
body.hero-anime h1 span:nth-child(3) {
  opacity: 0;
  transform: translateY(-50px);
}
body.hero-anime h1 span:nth-child(4) {
  opacity: 0;
  transform: translateY(-10px);
}
body.hero-anime h1 span:nth-child(5) {
  opacity: 0;
  transform: translateY(-50px);
}
body.hero-anime h1 span:nth-child(6) {
  opacity: 0;
  transform: translateY(-20px);
}
body.hero-anime h1 span:nth-child(7) {
  opacity: 0;
  transform: translateY(-40px);
}
body.hero-anime h1 span:nth-child(8) {
  opacity: 0;
  transform: translateY(-10px);
}
body.hero-anime h1 span:nth-child(9) {
  opacity: 0;
  transform: translateY(-30px);
}
body.hero-anime h1 span:nth-child(10) {
  opacity: 0;
  transform: translateY(-20px);
}
h1 span:nth-child(1) {
  transition-delay: 1000ms;
}
h1 span:nth-child(2) {
  transition-delay: 700ms;
}
h1 span:nth-child(3) {
  transition-delay: 900ms;
}
h1 span:nth-child(4) {
  transition-delay: 800ms;
}
h1 span:nth-child(5) {
  transition-delay: 1000ms;
}
h1 span:nth-child(6) {
  transition-delay: 700ms;
}
h1 span:nth-child(7) {
  transition-delay: 900ms;
}
h1 span:nth-child(8) {
  transition-delay: 800ms;
}
h1 span:nth-child(9) {
  transition-delay: 600ms;
}
h1 span:nth-child(10) {
  transition-delay: 700ms;
}
body.hero-anime h1 span:nth-child(11) {
  opacity: 0;
  transform: translateY(30px);
}
body.hero-anime h1 span:nth-child(12) {
  opacity: 0;
  transform: translateY(50px);
}
body.hero-anime h1 span:nth-child(13) {
  opacity: 0;
  transform: translateY(20px);
}
body.hero-anime h1 span:nth-child(14) {
  opacity: 0;
  transform: translateY(30px);
}
body.hero-anime h1 span:nth-child(15) {
  opacity: 0;
  transform: translateY(50px);
}
h1 span:nth-child(11) {
  transition-delay: 1300ms;
}
h1 span:nth-child(12) {
  transition-delay: 1500ms;
}
h1 span:nth-child(13) {
  transition-delay: 1400ms;
}
h1 span:nth-child(14) {
  transition-delay: 1200ms;
}
h1 span:nth-child(15) {
  transition-delay: 1450ms;
}
#switch,
#circle {
  cursor: pointer;
  -webkit-transition: all 300ms linear;
  transition: all 300ms linear;
}
#switch {
  width: 60px;
  height: 8px;
  border: 2px solid #8167a9;
  border-radius: 27px;
  background: #000;
  position: relative;
  display: block;
  margin: 0 auto;
  text-align: center;
  opacity: 1;
  transform: translate(0);
  transition: all 300ms linear;
  transition-delay: 1900ms;
}
body.hero-anime #switch {
  opacity: 0;
  transform: translateY(40px);
  transition-delay: 1900ms;
}
#circle {
  position: absolute;
  top: -11px;
  left: -13px;
  width: 26px;
  height: 26px;
  border-radius: 50%;
  background: #000;
}
.switched {
  border-color: #000 !important;
  background: #8167a9 !important;
}
.switched #circle {
  left: 43px;
  box-shadow: 0 4px 4px rgba(26, 53, 71, 0.25), 0 0 0 1px rgba(26, 53, 71, 0.07);
  background: #fff;
}
.nav-item .dropdown-menu {
  transform: translate3d(0, 10px, 0);
  visibility: hidden;
  opacity: 0;
  max-height: 0;
  display: block;
  padding: 0;
  margin: 0;
  transition: all 200ms linear;
}
.nav-item.show .dropdown-menu {
  opacity: 1;
  visibility: visible;
  max-height: 999px;
  transform: translate3d(0, 0px, 0);
}
.dropdown-menu {
  padding: 10px !important;
  margin: 0;
  font-size: 13px;
  letter-spacing: 1px;
  color: #212121;
  background-color: #fcfaff;
  border: none;
  border-radius: 3px;
  box-shadow: 0 5px 10px 0 rgba(138, 155, 165, 0.15);
  transition: all 200ms linear;
}
.dropdown-toggle::after {
  display: none;
}

.dropdown-item {
  padding: 3px 15px;
  color: #212121;
  border-radius: 2px;
  transition: all 200ms linear;
}
.dropdown-item:hover,
.dropdown-item:focus {
  color: #fff;
  background-color: rgba(129, 103, 169, 0.6);
}

body.dark {
  color: #fff;
  background-color: #1f2029;
}
body.dark .navbar-brand img {
  filter: brightness(100%);
}
body.dark h1 {
  color: #fff;
}
body.dark h1 span {
  transition-delay: 0ms !important;
}
body.dark p {
  color: #fff;
  transition-delay: 0ms !important;
}
body.dark .bg-light {
  background-color: #14151a !important;
}
body.dark .start-header {
  box-shadow: 0 10px 30px 0 rgba(0, 0, 0, 0.15);
}
body.dark .start-header.scroll-on {
  box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.15);
}
body.dark .nav-link {
  color: #fff !important;
}
body.dark .nav-item.active .nav-link {
  color: #999 !important;
}
body.dark .dropdown-menu {
  color: #fff;
  background-color: #1f2029;
  box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.25);
}
body.dark .dropdown-item {
  color: #fff;
}
body.dark .navbar-light .navbar-toggler-icon {
  border-bottom: 1px solid #fff;
}
body.dark .navbar-light .navbar-toggler-icon:after,
body.dark .navbar-light .navbar-toggler-icon:before {
  background-color: #fff;
}
body.dark .navbar-toggler[aria-expanded="true"] .navbar-toggler-icon {
  border-color: transparent;
}

/* #Media
================================================== */

@media (max-width: 767px) {
  h1 {
    font-size: 38px;
  }
  .nav-item:after {
    display: none;
  }
  .nav-item::before {
    position: absolute;
    display: block;
    top: 15px;
    left: 0;
    width: 11px;
    height: 1px;
    content: "";
    border: none;
    background-color: #000;
    vertical-align: 0;
  }
  .dropdown-toggle::after {
    position: absolute;
    display: block;
    top: 10px;
    left: -23px;
    width: 1px;
    height: 11px;
    content: "";
    border: none;
    background-color: #000;
    vertical-align: 0;
    transition: all 200ms linear;
  }
  .dropdown-toggle[aria-expanded="true"]::after {
    transform: rotate(90deg);
    opacity: 0;
  }
  .dropdown-menu {
    padding: 0 !important;
    background-color: transparent;
    box-shadow: none;
    transition: all 200ms linear;
  }
  .dropdown-toggle[aria-expanded="true"] + .dropdown-menu {
    margin-top: 10px !important;
    margin-bottom: 20px !important;
  }
  body.dark .nav-item::before {
    background-color: #fff;
  }
  body.dark .dropdown-toggle::after {
    background-color: #fff;
  }
  body.dark .dropdown-menu {
    background-color: transparent;
    box-shadow: none;
  }
}

.logo {
  position: fixed;
  bottom: 0;
  right: 0;
  // transform: translate(-50%, -50%);
  z-index: 9999;
}

.logo img {
  height: 250px;
  width: auto;
  display: block;
  /* filter: brightness(10%); */
  /* transition: all 250ms linear; */
}
// 위의 스타일을 HTML 파일에 적용하면 .logo 클래스를 가진 요소가 우측 하단에 고정되고, 이미지는 해당 스타일을 따라 크기 조정됩니다. position: fixed 속성은 요소를 고정 위치에 배치하며, bottom: 0과 right: 0 속성을 사용하여 우측 하단에 위치하도록 지정합니다. transform: translate(-50%, -50%);은 요소를 정확히 가운데로 이동시키는 역할을 합니다. z-index: 9999;는 다른 요소




body.dark .logo img {
  filter: brightness(100%);
}

.clock-container {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
}

.clock {
  width: 400px;
  height: 400px;
  border-radius: 50%;
  background-color: #fff;
  position: relative;
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.1);
  border: 2px solid rgba(100, 80, 80, 0.336);
}

.current-time {
  position: absolute;
  top: -40px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 24px;
  font-weight: bold;
}

.hand1 {
  transform: rotate(30deg);
  animation: rotate1 1s linear infinite;
}

.hand2 {
  transform: rotate(60deg);
  animation: rotate2 2s linear infinite;
}

.second-hand {
  background-color: #72c2f063;
  position: absolute;
  width: 3px;
  height: 120px;
  left: calc(50% - 3px);
  top: calc(50% - 120px);
  transform-origin: bottom center;
  z-index: 1;
}

.minute-hand {
  background-color: #0808085e;
  position: absolute;
  width: 6px;
  height: 140px;
  left: calc(50% - 4px);
  top: calc(50% - 140px);
  transform-origin: bottom center;
  z-index: 2;
}

.hour-hand {
  background-color: #0808085e;
  position: absolute;
  width: 5px;
  height: 120px;
  left: calc(50% - 5px);
  top: calc(50% - 120px);
  transform-origin: bottom center;
  z-index: 3;
}

@keyframes rotate1 {
  from {
    transform: rotate(30deg);
  }

  to {
    transform: rotate(390deg);
  }
}

@keyframes rotate2 {
  from {
    transform: rotate(60deg);
  }

  to {
    transform: rotate(420deg);
  }
}

</style>
