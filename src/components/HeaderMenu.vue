<template>
  <div>
    <ul class="list">
      <li>
        <a
          :class="{ 'list--item__active': activedSection === 'home' }"
          href="#home"
          @click="activedSection = 'home'"
          >INICIO</a
        >
      </li>
      <li>
        <a
          :class="{ 'list--item__active': activedSection === 'who-i-am' }"
          href="#who-i-am"
          @click="activedSection = 'who-i-am'"
          >QUIEN SOY</a
        >
      </li>
      <li>
        <a
          :class="{
            'list--item__active': activedSection === 'what-i-can-contribute',
          }"
          href="#what-i-can-contribute"
          @click="activedSection = 'what-i-can-contribute'"
          >QUE PUEDO APORTAR</a
        >
      </li>
      <li><a href="#">EXPERIENCIA</a></li>
      <li><a href="#">PROYECTOS</a></li>
    </ul>
    <img
      class="header__img"
      src="../assets/LogoPortFolio.png"
      alt="Juan Andrés Escobar Logo"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from "vue";
import { gsap } from "gsap";
export default defineComponent({
  name: "HeaderMenu",
  setup() {
    const activedSection = ref("");

    onMounted(() => {
      gsap.set(".list", {
        opacity: 0,
      });
      gsap.to(".list", {
        duration: 2,
        delay: 1,
        opacity: 1,
      });

      gsap.set(".header__img", {
        opacity: 0,
      });
      gsap.to(".header__img", {
        duration: 2,
        delay: 1,
        opacity: 1,
      });
    });
    return {
      activedSection,
    };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
div {
  z-index: 10;
  position: fixed;
  display: flex;
  justify-content: space-between;
  width: 100vw;
  align-items: center;

  ul {
    list-style: none;
    display: flex;
    flex-direction: column;
    justify-content: end;
    margin: 25px 15px 0 60px;
    li {
      a:hover {
        font-size: 18px;
        transition: 0.2s all ease-out;
      }
      a {
        opacity: 0.5;
        text-decoration: none;
        color: white;
        cursor: none !important;

        &.list--item__active {
          opacity: 1;
          font-weight: bold;
        }
      }
    }
  }
  img {
    margin: 35px 114px;
    width: 85px;
    height: 85px;
  }
}
</style>
