<template>
  <v-list
    v-editable="blok"
    :dark="blok.dark"
    :dense="blok.dense"
    :disabled="blok.disabled"
    :nav="blok.list_style==='nav'"
    :rounded="blok.list_style==='rounded'"
    :shaped="blok.list_style==='shaped'"
    :subheader="blok.subheader.length > 0"
    :three-line="blok.threeline"
    :two-line="blok.twoline"
    :class="[blok.helpers, blok.expand ? 'content-list' : '']"
    :style="blok.style"
  >
    <v-subheader v-if="blok.subheader">{{blok.subheader}}</v-subheader>
    <v-list-item-group
      v-model="item"
      :color="blok.color | lightOrDark(this.$vuetify.theme.dark)"
      :class="blok.grid_list ? 'grid-list' : ''"
      :style="gridStyles"
      :data-aos="blok.animate_list"
      data-aos-once="true"
    >
      <component
        :key="blok._uid"
        v-for="(blok, n) in blok.listcontent"
        :blok="blok"
        :is="blok.component | dashify"
        :style="`--animation-order: ${n};`"
      ></component>
      {{blok.text}}
    </v-list-item-group>
  </v-list>
</template>

<script>
export default {
  props: ["blok"],
  data: () => ({
    item: null
  }),
  computed: {
    gridStyles() {
      return `grid-template-columns: repeat(auto-fit, minmax(${this.blok.grid_column_width}px, 1fr)); gap: ${this.blok.grid_gap} ${this.blok.grid_gap};`;
    }
  }
};
</script>

// TODO: Allow dynamic animation setting
<style scoped>
.v-list {
  width: 100%;
}

.grid-list {
  display: grid;
  width: 100%;
}

.aos-animate * {
  animation-name: animateIn;
  animation-duration: 300ms;
  animation-delay: calc(var(--animation-order) * 200ms);
  animation-fill-mode: both;
  animation-timing-function: ease-in-out;
}

@keyframes animateIn {
  0% {
    opacity: 0;
    transform: scale(0.6) translateY(-8px);
  }

  100% {
    opacity: 1;
  }
}
</style>

<style lang="scss">
.v-navigation-drawer__content .v-list {
  background: transparent;
}
.content-list {
  .v-list-item {
    &__title,
    &__subtitle,
    &__content {
      -webkit-line-clamp: unset;
      overflow: visible;
      text-overflow: auto;
      white-space: unset;
    }
  }
}
</style>
