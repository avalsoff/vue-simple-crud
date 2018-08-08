<template>
  <form>
    <div class="form-group">
      <label for="productName">Product name</label>
      <input 
        type="text" 
        v-model="product.name" 
        id="productName" 
        class="form-control" 
        maxlength="32" 
        placeholder="Enter product name">
    </div>
    <div class="form-group">
      <label for="productDescription">
        Product description <small class="text-muted">(optional)</small>
      </label>
      <textarea 
        v-model="product.description" 
        id="productDescription" 
        class="form-control" 
        rows="3" 
        maxlength="128" 
        placeholder="Enter description"
      ></textarea>
    </div>
    <div class="form-group">
      <label for="price">Price</label>
      <input 
        type="number" 
        v-model="product.price" 
        id="price" 
        class="form-control" 
        placeholder="Enter Price" 
        number
      >
    </div>
    <button 
      type="submit" 
      @click.prevent="submit" 
      class="btn btn-success"
    >
      {{ isEditing ? 'Update product' : 'Add product' }}
    </button>
    <button
      v-show="isEditing"
      type="reset"
      @click.prevent="cancel"
      class="btn btn-danger ml-3"
    >
      Cancel
    </button>
  </form>  
</template>

<script>
export default {
  data () {
    return {
      formErrors: [],
    };
  },
  
  props: {
    product: {
      type: Object,
    },
    isEditing: {
      type: Boolean,
      default: false,
    },
  },

  watch: {
    'product.id' () {
      this.formErrors = {};
    },
  },

  methods: {
    submit () {
      if ( this.validateForm() ) {
        this.$emit('submit', this.product);
      }
    },

    cancel () {
      this.formErrors = {};
      this.$emit('cancel', this.product);
    },

    validateForm () {
      const errors = [];

      if (!this.product.name) {
        errors.push('Name is required');
      }

      if (!this.product.price) {
        errors.push('Price is required');
      }

      this.formErrors = errors;

      return errors.length === 0;
    },
  },
}
</script>

<style lang="scss" scoped>
form {
  margin-bottom: 16px;
}
</style>

