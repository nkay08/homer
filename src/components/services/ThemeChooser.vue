<template>
  <Generic :item="item">
    <template #content>
      <p class="title is-4">{{ item.name }}</p>
      <p class="subtitle is-6">
        <template v-if="item.subtitle">
          {{ item.subtitle }}
        </template>
        <select v-model="theme" @change="switchTheme">
          <option>classic</option>
          <option>neon</option>
          <option>walkxcode</option>
        </select>
      </p>
    </template>
  </Generic>
</template>

<script>
import Generic from "./Generic.vue";

let currentTheme;
const app = document.getElementById("app");

export default {
  name: "ThemeChooser",
  props: {
    item: Object,
  },
  components: {
    Generic,
  },
  data: () => {
    return {
      theme: null,
    };
  },
  created: function () {
    currentTheme = Array.from(app.classList).filter(word => word.startsWith("theme-"))[0];
  },
  methods: {
    switchTheme: function () {
      const newTheme = `theme-${this.theme}`;
      app.classList.replace(currentTheme, newTheme);
      currentTheme = newTheme;
    },
  },
};
</script>
