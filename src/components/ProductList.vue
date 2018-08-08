<template>
<table class="table table-hover product-table">
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr
      v-for="product in products"
      track-by="id"
      :key="product.id"
      @click.prevent="edit(product)"
    >
      <td>{{ product.name }}</td>
      <td>{{ product.description }}</td>
      <td>{{ product.price }}:-</td>
      <td><a href="#" @click.prevent.stop="remove(product.id)">remove</a></td>
    </tr>
  </tbody>
</table>
</template>

<script>
export default {
  props: {
    products: {
      type: Array
    },
  },
  methods: {
    edit (product) {
      this.$emit('edit', product);
    },
    remove (id) {
      this.$emit('remove', id);
    },
  },
};
</script>

<style lang="scss" scoped>
.header {
  font-size: 4rem;
}
</style>
