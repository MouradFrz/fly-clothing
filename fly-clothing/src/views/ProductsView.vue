<template>
  <div class="filter container-md">
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid d-flex justify-content-start">
        <div class="filter-container">
        <label for="model">Model :</label>
        <select id="model" class="form-select" v-model="model" aria-label="Model">
          <option value="">Any</option>
          <option value="Air jordan 1">Air Jordan 1</option>
          <option value="Tn">Tn</option>
          <option value="Air max">Air Max</option>
        </select>
        </div>
        <div class="filter-container">
        <label for="color">Color:</label>
        <select id="color" class="form-select" v-model="color" aria-label="Color">
          <option value="">Any</option>
          <option value="Blue">Blue</option>
          <option value="Red">Red</option>
          <option value="Brown">Brown</option>
          <option value="Rainbow">Rainbow</option>
          <option value="Gray">Gray</option>
          <option value="White">White</option>
        </select>
</div>
        <!-- <button class="btn btn-outline-success align-self-end" @click="filter">Filter</button> -->
      </div>
    </nav>
  </div>
  <div class="products container-md">
    <h1 v-if="notAvailable">No items matching the necessary conditions</h1>
    <div class="row g-4">
      <div
        class="col-12 col-sm-6 col-md-4 col-lg-3"
        v-for="(card, i) in changableList"
        key="i"
      >
        <div class="card justify-content-between">
          <img :src="card.imgsrc" class="card-img-top" alt="..." />
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
.filter-container{
  margin-right: 40px;
  width: 200px;
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
      color: "",
      changableList: this.productsList,
      notAvailable: false
    };
  },
  methods: {
    shuffle(array) {
  array.sort(() => Math.random() - 0.5);
},
    filter() {
      let result = [];
      if (this.model == "" && this.color == "") {
        result = this.productsList;
      } else if (this.model == "") {
        this.productsList.forEach((element) => {
          if (element.color === this.color) {
            result.push(element);
          }
        });
      } else if (this.color == "") {
        this.productsList.forEach((element) => {
          if (element.model === this.model) {
            result.push(element);
          }
        });
      } else {
        this.productsList.forEach((element) => {
          if ((element.model === this.model) & (element.color === this.color)) {
            result.push(element);
          }
        });
      }
      this.shuffle(result)
      this.changableList = result;
      if(result.length == 0){
        this.notAvailable=true
      }else{
        this.notAvailable=false
      }
    },
  },
  watch:{
    model(newval,oldval){
      this.filter()
    },
    color(newval,oldval){
      this.filter()
    }
  },
  mounted(){
    this.shuffle(this.changableList)
  },
  props: ["productsList"],
};
</script>