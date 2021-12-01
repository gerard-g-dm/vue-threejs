<template>
<div>
  <navigation-header></navigation-header>
  <div class="container" id="product-list">
    <div class="row row-cols-1 row-cols-sm-2 row-cols-md-2 g-3">
      <div
        class="col p-5"
        v-for="(product, index) in productList"
        v-bind:key="'product-item-' + product.title.replace(' ', '-')"
      >
        <product-thumbnail
          v-bind:key="product.title"
          :product="product"
          :thumbnail-id="'thumbnail-' + index"
        ></product-thumbnail>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import ProductThumbnail from "../../components/product-thumbnail/product-thumbnail";
import NavigationHeader from "../../components/navigation-header/navigation-header";

export default {
  name: "ProductList",
  components: {
    ProductThumbnail,
    NavigationHeader
  },
  data() {
    return {
      productList: [
        {
          title: "helmet example",
          description: `Donec vestibulum mauris eu quam rhoncus, sed iaculis urna feugiat. Maecenas vehicula nisl elit, quis. `,
          obj3DSettings: {
            link: "/static/assets/models/gltf/helmet/DamagedHelmet.gltf",
            cameraPosition: [-1.8, 0.6, 2.7]
          }
        },
        {
          title: "car example",
          description: `In nec fringilla neque, non ullamcorper nibh. Suspendisse potenti. Pellentesque luctus pulvinar hendrerit. In interdum.`,
          obj3DSettings: {
            link: "/static/assets/models/gltf/car/nissan-skyline/scene.gltf",
            cameraPosition: [-0.8, 0.6, 0.7],
            scale: 0.0005
          }
        },
        {
          title: "car example 2",
          description: `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed tortor elit, convallis ac orci non.`,
          obj3DSettings: {
            link:
              "/static/assets/models/gltf/car/chevrolet-corvette/scene.gltf",
            cameraPosition: [-1.8, 0.6, 2.7],
            scale: 0.002
          }
        }
      ]
    };
  }
};
</script>
