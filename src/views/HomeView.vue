<template>
  <div class="c-cursor | js-cursor">
    <div class="c-cursor__inner"></div>
  </div>
  <HeaderMenu />
  <div class="home" id="home">
    <div class="section | home--title">
      <h2>
        フ <br />
        ア <br />
        ン <br />
        ・ <br />
        エ <br />
        ス <br />
        コ <br />
        バ <br />
        ル <br />
      </h2>
      <h1>
        <span class="letter__one">{{ myWord }}</span> <br />
        U <br />
        A <br />
        N <br />
        <br />
        E <br />
        S <br />
        C <br />
        O <br />
        B <br />
        A <br />
        R <br />
      </h1>
    </div>
    <div class="home--icons">
      <i class="fa-brands fa-linkedin"></i>
      <i class="fa-brands fa-github"></i>
      <i class="fa-solid fa-rectangle-code"></i>
    </div>
    <div class="home--scroll-indicator">
      <p>&copy; 2023 - Juan Escobar</p>
    </div>
  </div>
  <div class="section | who-i-am" id="who-i-am">
    <div class="who-i-am__description">
      <p>
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Eligendi
        similique magni id consequatur molestias at debitis repudiandae pariatur
        modi dolorum minus, maiores, adipisci perspiciatis distinctio, aperiam
        consequuntur ducimus! Facilis, alias! Libero, asperiores? Doloremque
        incidunt dolor provident tempora suscipit, dignissimos officia eum
        asperiores atque quisquam cum et voluptas illo. Beatae sint quam est
        molestias, veniam sit nobis perspiciatis tempore obcaecati consequatur?
        Mollitia, aliquam? Ab et ratione architecto quisquam? Amet quod vel
        totam, numquam ducimus laboriosam temporibus neque mollitia ea eos
        suscipit hic cum, esse eveniet debitis magni, rem nihil odio minus.
      </p>
    </div>
  </div>

  <div class="section | what-i-can-contribute" id="what-i-can-contribute">
    <div class="what-i-can-contribute__description">
      <p>Hola my friend</p>
    </div>
  </div>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";
import HeaderMenu from "../components/HeaderMenu.vue";
// import { gsap } from "gsap";
// import ScrollTrigger from "gsap/dist/ScrollTrigger";

export default defineComponent({
  name: "HomeView",
  components: {
    HeaderMenu,
  },
  setup() {
    const myWord = ref("J");
    let cursorEl;
    const isClickedClass = "is-clicked";
    const isHiddenClass = "is-hidden";
    const isLinkHoveredClass = "is-link-hovered";
    const hasCustomCursorClass = "has-custom-cursor";

    // const opacity = ref(1);
    // const beforeScroll = ref(0);
    onMounted(() => {
      document.body.classList.add(hasCustomCursorClass);
      setTimeout(() => {
        cursorEl = document.querySelector(".js-cursor");
      }, 100);
      addEventListeners();

      ramdomLetter();
    });

    const ramdomLetter = () => {
      const letters = [
        "A",
        "B",
        "C",
        "D",
        "E",
        "F",
        "G",
        "H",
        "I",
        "J",
        "K",
        "L",
        "M",
        "N",
        "Ñ",
        "O",
        "P",
        "Q",
        "R",
        "S",
        "T",
        "U",
        "V",
        "W",
        "X",
        "Y",
        "Z",
      ];

      let iterations = 0;
      const interval = setInterval(() => {
        myWord.value = myWord.value
          .split("")
          .map(() => letters[Math.floor(Math.random() * 26)])
          .join("");

        if (iterations >= 20) {
          myWord.value = "J";
          clearInterval(interval);
        }

        iterations += 1;
      }, 50);
    };

    const addEventListeners = () => {
      document.addEventListener("mousemove", onMouseMove);
      document.addEventListener("mousedown", onMouseDown);
      document.addEventListener("mouseup", onMouseUp);
      document.addEventListener("mouseenter", onMouseEnter);
      document.addEventListener("mouseleave", onMouseLeave);

      handleLinkHoverEvents();
    };

    const onMouseMove = (e) => {
      cursorEl.style.setProperty("--cursor-x", e.clientX + "px");
      cursorEl.style.setProperty("--cursor-y", e.clientY + "px");
    };

    const onMouseDown = () => {
      cursorEl.classList.add(isClickedClass);
    };

    const onMouseUp = () => {
      cursorEl.classList.remove(isClickedClass);
    };

    const onMouseEnter = () => {
      cursorEl.classList.remove(isHiddenClass);
    };

    const onMouseLeave = () => {
      cursorEl.classList.add(isHiddenClass);
    };

    const handleLinkHoverEvents = () => {
      document
        .querySelectorAll(
          'a, button, .js-link, input[type="button"], input[type="submit"]'
        )
        .forEach((el) => {
          el.addEventListener("mouseover", () =>
            cursorEl.classList.add(isLinkHoveredClass)
          );
          el.addEventListener("mouseout", () =>
            cursorEl.classList.remove(isLinkHoveredClass)
          );
        });
    };

    // const onScroll = () => {
    //   window.addEventListener("scroll", handleScroll);
    // };

    // const handleScroll = () => {
    //   const currentScrollY = window.scrollY;

    //   if (currentScrollY > beforeScroll.value) {
    //     console.log(opacity.value);
    //     opacity.value -= 0.1;
    //   }

    //   beforeScroll.value = currentScrollY;
    // };

    return {
      myWord,
    };
  },
});
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP&display=swap");
$cursorSize: 10px;

.home--title {
  display: flex;
  width: 100%;
  height: 100vh;
  justify-content: center;
  align-items: center;

  h1 {
    text-align: center;
    border-left: 3px solid #c22918;
    padding-left: 30px;
  }

  h2 {
    font-family: "Noto Sans JP", sans-serif;
    color: black;
    margin-right: 30px;
  }
}

.home--icons {
  position: absolute;
  bottom: 0;
  margin: 0 0 40px 100px;
  animation: 3s opacity;

  i {
    color: white;
    font-size: 30px;
    margin-left: 10px;
  }
}

.home--scroll-indicator {
  font-weight: bold;
  color: white;
  position: absolute;
  bottom: 0;
  right: 0;
  margin: 0 100px 30px 0;
  animation: 3s opacity;
}

@keyframes opacity {
  0% {
    opacity: 0;
  }
  15% {
    opacity: 0;
  }
  30% {
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}
.c-cursor {
  position: fixed;
  width: $cursorSize;
  height: $cursorSize;
  top: calc($cursorSize / -2);
  left: calc($cursorSize / -2);
  transform: translate(var(--cursor-x, -100px), var(--cursor-y, -100px))
    translateZ(0);
  // transform: translate(-100px, -100px) translateZ(0);
  pointer-events: none;
  transition: none;
  z-index: 11000;
  will-change: transform;

  &__inner {
    display: block;
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-color: white;
    transition: all 0.15s ease-in-out;
    opacity: 1;
    transform: scale(1) translateZ(0);
    box-shadow: 0px 0px 17px 14px rgba(255, 255, 255, 0.1);
  }
  &.is-clicked {
    .c-cursor__inner {
      opacity: 0.5;
    }
  }

  &.is-hidden {
    .c-cursor__inner {
      opacity: 0;
    }
  }

  &.is-link-hovered {
    cursor: none !important;
    .c-cursor__inner {
      cursor: none !important;
      background-color: transparent;
      border: 1px solid white;
      box-shadow: 0px 0px 17px 14px rgba(255, 255, 255, 0.1);
    }
  }
}

.has-custom-cursor {
  &,
  * {
    cursor: none !important;
  }
}

.who-i-am {
  height: 100vh;
  widows: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
