<template>
  <div class="home">
    <ManageProducts />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
import ManageProducts from '@/components/ManageProducts.vue';

export default {
  name: 'home',
  components: {
    HelloWorld,
    ManageProducts,
  },
};
</script>
