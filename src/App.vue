<template>
  <div class="corpo">
    <meu-menu></meu-menu>

    <transition name="pagina-fade">
      <router-view></router-view>
    </transition>
  </div>
</template>

<script>
import Menu from './components/shared/menu/Menu.vue';

export default {
  components: {
    'meu-menu': Menu
  }
}
</script>

<style scoped>
  .corpo {
    font-family: Helvetica, sans-serif;
    margin: 0 auto;
    width: 96%;
  }

  .pagina-fade-enter, .pagina-fade-leave-active {
    opacity: 0;
  }

  .pagina-fade-enter-active, .pagina-fade-leave-active {
    transition: opacity 500ms;
  }
</style>
