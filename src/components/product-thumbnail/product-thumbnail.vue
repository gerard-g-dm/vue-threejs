<template>
  <div class="card shadow-sm">
    <div class="product-content">
      <div class="bd-placeholder-img card-img-top product-thumbnail" :id="thumbnailId">
        <product-view
          :container-id="thumbnailId"
          :model-settings="product.obj3DSettings"
        ></product-view>
      </div>
      <div class="card-body">
        <div class="card-text">
          <div class="title">{{ product.title }}</div>
          {{ product.description }}
        </div>
        <div class="d-flex justify-content-between align-items-center">
          <div class="btn-group">
            <button class="btn btn-sm btn-outline-secondary" type="button">Nous contacter</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ProductView from "../product-view/product-view";

export default {
  name: "ProductThumbnail",
  components: {
    ProductView
  },
  props: {
    product: {
      type: Object,
      required: true
    },
    thumbnailId: {
      type: String,
      required: true
    }
  }
};
</script>


<style>
.product-thumbnail {
  width: 100%;
  height: 400px;
}
.title {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 50px;
  text-align: center;
  border-bottom: 1px solid #ccc;
}
</style>
