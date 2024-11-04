<template>
  <div class="container">
    <ul :class="['menu', { active: isActive }]">
      <div class="toggle" @click="toggleMenu">
        <Icon icon="ion:add-outline" />
      </div>
      <li
        v-for="(icon, index) in icons"
        :key="index"
        :style="{ '--i': index }"
        :class="{ active: index === activeIndex }"
        @click="setActive(index)"
      >
        <a :href="icon.url">
          <Icon :icon="icon.name" />
        </a>
      </li>
      <div class="indicator"></div>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { Icon } from '@iconify/vue';

const isActive = ref(false);
const activeIndex = ref(0);

const icons = [
  { name: 'ion:home-outline', url: '#' },
  { name: 'ion:person-outline', url: '#' },
  { name: 'ion:chatbubble-outline', url: '#' },
  { name: 'ion:mail-outline', url: '#' },
  { name: 'ion:videocam-outline', url: '#' },
  { name: 'ion:camera-outline', url: '#' },
  { name: 'ion:settings-outline', url: '#' },
  { name: 'ion:key-outline', url: '#' },
];

const toggleMenu = () => {
  isActive.value = !isActive.value;
};

const setActive = (index) => {
  activeIndex.value = index;
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  position: fixed;
  top: 20px;
  right: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.menu {
  position: relative;
  width: 300px;
  height: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.menu .toggle {
  position: absolute;
  width: 75px;
  height: 75px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #222;
  background: #fff;
  font-size: 3em;
  cursor: pointer;
  border-radius: 50%;
  transition: 0.5s;
}

.menu .toggle.active {
  transform: rotate(315deg);
  box-shadow: 0 0 0 68px #fff;
  color: #fff;
  background: #222237;
}

.menu li {
  position: absolute;
  left: 10px;
  list-style: none;
  transform: rotate(calc(360deg / 8 * var(--i))) translateX(40px);
  transform-origin: 140px;
  visibility: hidden;
  opacity: 0;
  z-index: 10;
  transition: 0.5s;
}

.menu.active li {
  visibility: visible;
  color: green;
  opacity: 1;
}

.menu li a {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 55px;
  height: 55px;
  font-size: 1.75em;
  transform: rotate(calc(360deg / -8 * var(--i)));
  border-radius: 50%;
  color: whitesmoke;
}

.menu.active li.active {
  transform: rotate(calc(360deg / 8 * var(--i))) translateX(12px);
}

.menu.active li.active a{
  color: skyblue;
}

.indicator {
  position: absolute;
  left: calc(50% - 2.5px);
  transform-origin: right;
  width: 100px;
  height: 1px;
  background: transparent;
  pointer-events: none;
  transition: 0.5s;
}

.indicator::before {
  content: "";
  position: absolute;
  top: -27px;
  left: 72px;
  width: 55px;
  height: 55px;
  background: #222237;
  border-radius: 50%;
  box-shadow: 0 0 0 6px #29fd53;
  opacity: 0;
  transition: 0.5s;
}

.menu.active .indicator::before {
  opacity: 1;
  top: -27.5px;
  left: -25px;
  background: lightblue;
  box-shadow: 0 0 0 6px #222237;
}
</style>
