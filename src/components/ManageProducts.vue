<template>
  <section>
    <ProductSaveForm
      :product="productInForm"
      :isEditing="isEditing"
      @submit="saveForm"
      @cancel="resetForm"
    />
    <ProductList
      v-if="products.length"
      :products="products"
      @edit="editProduct"
      @remove="removeProduct"
    />
  </section>
</template>

<script>
import uuid from 'uuid';

import ProductList from './ProductList';
import ProductSaveForm from './ProductSaveForm';

const initialData = {
  id: null,
  name: '',
  description: '',
  price: null,
}

export default {
  components: {
    ProductList,
    ProductSaveForm,
  },  
  data() {
    return {
      isEditing: false,
      productInForm: { ...initialData },
      products: [
        {
          id: 'cc919e21-ae5b-5e1f-d023-c40ee669520c',
          name: 'COBOL 101 vintage',
          description: 'Learn COBOL with this vintage programming book',
          price: 399,
        },
        {
          id: 'bcd755a6-9a19-94e1-0a5d-426c0303454f',
          name: 'Sharp C2719 curved TV',
          description: 'Watch TV like never before with the brand new curved screen technology',
          price: 1995,
        },
        {
          id: '727026b7-7f2f-c5a0-ace9-cc227e686b8e',
          name: 'Remmington X mechanical keyboard',
          description: 'Excellent for gaming and typing, this Remmington X keyboard ' +
            'features tactile, clicky switches for speed and accuracy',
          price: 595,
        },
      ],
    };
  },
  methods: {
    // Pass object by value
    saveForm ({ ...product }) {
      const index = this.products.findIndex(p => p.id === product.id);

      // If id in form already exists in list of products, update product
      // else add new product
      if (index !== -1) {
        this.products.splice(index, 1, product);
      } else {
        product.id = uuid.v4();
        this.products.push(product);
      }

      this.resetForm();
    },
    editProduct ({ ...product }) {
      this.productInForm = product;
      this.isEditing = true;
    },
    removeProduct (id) {
      this.products = this.products
        .filter(p => p.id !== id);

      if (id === this.productInForm.id) {
        this.resetForm();
      }
    },
    resetForm () {
      this.productInForm = initialData;
      this.isEditing = false;
    },
  },
}
</script>