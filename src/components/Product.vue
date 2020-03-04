<template>
  <div class="product">
    <img v-bind:src="product.image" />
    <div class="footer">
      <h3>{{ product.title }}</h3>
      <p>£{{ product.price / 100.0 }}</p>
      <span class="desc">{{ product.description }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: {
    product: { type: Object, required: true }
  }
};
</script>

<style lang="scss">
@font-face {
  font-family: "Gilroy";
  src: url("../assets/Gilroy-Light.otf") format("opentype");
}

.product {
  width: 260px; // 465 // 325
  max-height: 195px; // 350 // 244
  position: relative;

  img {
    width: 100%;
    border-radius: 8px;
  }

  .footer {
    position: absolute;
    bottom: 0;
    width: 100%;
    color: white;
    background: rgba(40, 40, 40, 0.8);
    border-radius: 0px 0px 8px 8px;
    padding: 16px;

    /* Pica */
    font-family: Gilroy;
    font-style: normal;
    font-weight: 600;
    font-size: 16px;
    line-height: 19px;
    text-align: left;

    h3,
    p {
      padding: 0;
      margin: 0;
      margin-bottom: 8px;
    }
    .desc {
      /* Minion */
      font-weight: 500;
      font-size: 12px;
      line-height: 14px;
    }
  }
}
</style>
