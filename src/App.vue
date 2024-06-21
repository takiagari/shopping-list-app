<template>
  <div id="app">
    <!-- ShoppingListAppコンポーネントの呼び出し -->
    <ShoppingListApp />
  </div>
</template>

<script>
import ShoppingListApp from './components/ShoppingListApp.vue';

export default {
  name: 'App',
  components: {
    ShoppingListApp
  }
};
</script>
