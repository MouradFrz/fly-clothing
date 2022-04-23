<template>
  <div class="filter container-md">
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid">
        <select class="form-select w-25" v-model="model" aria-label="Model">
          <option selected>Model</option>
          <option value="Air jordan 1">Air Jordan 1</option>
          <option value="Tn">Tn</option>
          <option value="Air max">Air Max</option>
        </select>
        <!-- <select class="form-select w-25" aria-label="Model">
          <option selected>Model</option>
          <option value="1">Air Jordan 1 </option>
          <option value="2">Tn</option>
          <option value="3">Air Max</option>
        </select> -->
        <button class="btn btn-outline-success" @click="filter">Filter</button>
      </div>
    </nav>
  </div>
  <div class="products container-md">
    <div class="row g-4">
      <div
        class="col-12 col-sm-6 col-md-4 col-lg-3"
        v-for="(card, i) in changableList"
        key="i"
      >
        <div class="card justify-content-between">
          <img :src="images[i]" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title text-primary">{{ card.model }}</h5>
            <h5 class="card-title">Color:{{ card.color }}</h5>
            <a href="#" class="btn btn-primary">Add to cart</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style lang="scss">
.products {
  background-color: rgb(231, 231, 231) !important;
}
.card {
  height: 100%;
}
.card-body {
  flex: 0 !important;
}
</style>

<script>
export default {
  data() {
    return {
      images: [],
      model: "",
      changableList: this.productsList,
    };
  },
  methods: {
    filter() {
      let result = [];
      this.productsList.forEach((element) => {
        if (element.model === this.model) {
          result.push(element);
        }
      });
      this.changableList = result;
    },
  },

  props: ["productsList"],
  async mounted() {
    this.changableList.forEach((element, i) => {
      this.images[i] = element.imgsrc;
    });
  },
};
</script>