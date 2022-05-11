<template>
  <div class="filter container-md">
    <nav class="navbar navbar-light">
      <div class="container-fluid d-flex justify-content-start bg-main m-0">
        <div class="filter-container">
          <label for="model">Model :</label>
          <select
            id="model"
            class="custom-select"
            v-model="model"
            aria-label="Model"
          >
            <option value="">Any</option>
            <option value="Air jordan 1">Air Jordan 1</option>
            <option value="Tn">Tn</option>
            <option value="Air max">Air Max</option>
            <option value="Dunks">Dunks</option>
          </select>
        </div>
        <div class="filter-container">
          <label for="color">Color:</label>
          <select
            id="color"
            class="custom-select"
            v-model="color"
            aria-label="Color"
          >
            <option value="">Any</option>
            <option value="Blue">Blue</option>
            <option value="Red">Red</option>
            <option value="Brown">Brown</option>
            <option value="Rainbow">Rainbow</option>
            <option value="Gray">Gray</option>
            <option value="White">White</option>
          </select>
        </div>
        <div class="filter-container">
          <label for="minPrice">Minimum price:</label>
          <input
            id="minPrice"
            type="number"
            min="0"
            class="custom-select"
            v-model="minPrice"
            aria-label="minPrice"
          />
        </div>
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
          <img :src="card.imgsrc" class="card-img-top" style="margin:auto;" alt="..." />
          <div class="card-body">
            <h5 class="card-title text-dark">{{ card.brand }} {{ card.model }}</h5>
            <h6 class="card-titl text-muted fw-light">
              Color: {{ card.color }}
            </h6>
            <h6 class="card-titl text-muted">Price: ${{ card.price }}</h6>
            <button class="btn btn-success" @click="add(card.id)" >Add to cart</button>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>


<style lang="scss" scoped>

option{
  background-color: rgb(255, 255, 255);
  border: none;
}
.filter-container {
  margin-right: 40px;
  width: 200px;
}
.card {
  height: 100%;
  border-bottom:1px solid red !important; 
  
}
.card-body {
  flex: 0 !important;
  border-right:1px solid red !important; 
 
}
.card-img-top{
 
}
.custom-select{
  padding: 6px;
  width: 100%;
  border: none;
  border-right:2px solid red !important;
  &:focus{
    outline: none;
    background-color: rgb(228, 228, 228);
  }
}
</style>

<script>

export default {
  
  data() {
    return {
      images: [],
      model: "",
      color: "",
      minPrice: 0,
      changableList: this.productsList,
      notAvailable: false,
      
    };
  },
  methods: {
    
    shuffle(array) {
      array.sort(() => Math.random() - 0.5);
    },
    filter() {
      let result = [];
      if (this.model == "" && this.color == "" && this.minPrice == 0) {
        result = this.productsList;
      } else if (this.model == "" && this.minPrice == 0) {
        this.productsList.forEach((element) => {
          if (element.color === this.color) {
            result.push(element);
          }
        });
      } else if (this.model == "" && this.color == "") {
        this.productsList.forEach((element) => {
          if (element.price >= this.minPrice) {
            result.push(element);
          }
        });
      } else if (this.color === "" && this.minPrice == 0) {
        this.productsList.forEach((element) => {
          if (element.model === this.model) {
            result.push(element);
          }
        });
      } else if (this.model == "") {
        this.productsList.forEach((element) => {
          if (element.color === this.color && element.price >= this.minPrice) {
            result.push(element);
          }
        });
      } else if (this.minPrice == 0) {
        this.productsList.forEach((element) => {
          if (element.color === this.color && element.model === this.model) {
            result.push(element);
          }
        });
      } else if (this.color == "") {
        this.productsList.forEach((element) => {
          if (element.model === this.model && element.price >= this.minPrice) {
            result.push(element);
          }
        });
      } else {
        this.productsList.forEach((element) => {
          if (element.model === this.model && element.color === this.color && element.price >= this.minPrice ) {
            result.push(element);
          }
        });
      }
      this.shuffle(result);
      this.changableList = result;
      if (result.length == 0) {
        this.notAvailable = true;
      } else {
        this.notAvailable = false;
      }
    },
  },
  watch: {
    model(newval, oldval) {
      this.filter();
    },
    color(newval, oldval) {
      this.filter();
    },
    minPrice(newval, oldval) {
      this.filter();
    },
  },
  mounted() {
    this.shuffle(this.changableList);
  },
  props: ["productsList","add"],
};
</script>